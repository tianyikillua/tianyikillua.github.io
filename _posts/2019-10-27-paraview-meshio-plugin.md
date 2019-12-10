---
title: Generic mesh readers under ParaView via the new Python interface
tags:
  - ParaView
  - Python
words_per_minute: 150
---
**中文简介** 这篇博文介绍了如何用 Python 库 [meshio](https://github.com/nschloe/meshio) 扩充 ParaView 可读取网格的格式。在 ParaView 5.7 版本下（或以前），存在一些 ParaView 本身不能读取的网格格式，比如 Abaqus (`.inp`), GMSH (`.msh`) 或者 MED (`.med`)。使用 ParaView 5.6 版本引进的新插件 Python 开发环境 `VTKPythonAlgorithmBase`，我最近开发了一个连接 meshio 与 ParaView 的插件，发布在 [Github](https://github.com/tianyikillua/paraview-meshio-reader) 上。
{: .notice--info}

Recently I discoved the Python `VTKPythonAlgorithmBase` interface introduced in the [ParaView 5.6 version](https://blog.kitware.com/paraview-5-6-0-release-notes/) for defining user plugins with pure Python files. These plugins can then be loaded through *Tools / Manage Plugins / Load New* under ParaView and can be served as custom sources, readers, writers and filters.

<img src="/assets/images/2019/10/paraview_plugins.png" width="912px" />

Previously before 5.6 only plugins defined by a XML file (or compiled library files) can be loaded. For generating such XML files, I used a Python package [pvpyfilter](https://github.com/shuhaowu/pvpyfilter). With the newly introduced native `VTKPythonAlgorithmBase` interface, it is no longer necessary.

In this post, I will illustrate the development of such Python plugins via the example of a generic mesh format reader, with the help of [meshio](https://github.com/nschloe/meshio). The code source of this plugin is available on [Github](https://github.com/tianyikillua/paraview-meshio-reader).

## [meshio](https://github.com/nschloe/meshio)

[meshio](https://github.com/nschloe/meshio) is a Python library that reads and writes various frequently-used mesh formats: XDMF, VTK, gmsh, Abaqus...Personnally since 2018 I'm actively involved in this project especially for the MED format. The finite element result produced by [code_aster](https://www.code-aster.org/spip.php?rubrique1) is a MED file and in general requires the rather fatty [salome platform](https://www.salome-platform.org/) for visualization and post-processing. With the MED interface of meshio, these results files can now be converted to a more generic format readable directly by ParaView, like XDMF or VTU. Directly Python processing is also possible without the use of salome environment.

The API of meshio is minimalist. For reading or writing a mesh file `foo`, simply use
``` python
mesh = meshio.read(foo)  # read mesh from foo
meshio.write(foo, mesh)  # write mesh to foo
```
The actual mesh format used by `foo` is either automatically deduced from its extension, or in case of ambiguity, can be specified by the `file_format` argument
``` python
mesh = meshio.read(foo, file_format="...")
meshio.write(foo, mesh, file_format="...")
```

The mesh information is contained in a `Mesh` instance returned by `meshio.read`. The most useful attributes are defined as follows
``` python
mesh.points  # node coordinates
mesh.cells  # cell connectivities
mesh.point_data  # nodal fields
mesh.cell_data  # cell fields
```
For cells, `mesh.cells` is a dictionary that defines the connectivity information for each geomerical type of cells. In the case of a 2d mesh composed of triangles and quads, we will have
``` python
mesh.cells = {
    "triangle": ...,  # a (n_triangles, 3) numpy array
    "quad": ...,  # a (n_quads, 4) numpy array
}
```
Each line of these two numpy arrays specifies the node id's of a particular cell: 3 points for triangles and 4 for quad's. The id's correspond to the node coordinates of the mesh defined in `mesh.points`.

The point data is a dictionary of numpy arrays with the keys as field names, for instance
``` python
mesh.point_data = {
    "Displacement": ...,  # a (n_points, 3) numpy array
}
```
defines a 3d (with 3 spatial components) displacement field defined on each node of the mesh. As for cell data, an additional dictionary level is necessary to specify the cell type
``` python
mesh.cell_data = {
    "triangle":  {
        "Displacement": ...,  # a (n_triangles, 3) numpy array
    },
    "quad":  {
        "Displacement": ...,  # a (n_quads, 3) numpy array
    },
}
```
In this case, a 3d displacement is defined on each triangular and quadrilateral cell.

## `VTKPythonAlgorithmBase` interface for defining ParaView plugins

For a more comprehensive introduction, interested readers can consult section 12.4 of the [ParaView Guide](https://www.paraview.org/paraview-guide/) and the [PythonAlgorithmExamples.py](https://gitlab.kitware.com/paraview/paraview/blob/master/Examples/Plugins/PythonAlgorithm/PythonAlgorithmExamples.py) file provided by ParaView.

Essentially, to develop a user ParaView plugin, we just need to define a subclass of  `VTKPythonAlgorithmBase` in your Python file. In my generic mesh reader case, we have
``` python
from paraview.util.vtkAlgorithm import VTKPythonAlgorithmBase
class meshioReader(VTKPythonAlgorithmBase):
    def __init__(self):
        VTKPythonAlgorithmBase.__init__(
            self, nInputPorts=0, nOutputPorts=1, outputType="vtkUnstructuredGrid"
        )
        ...
```
If you are familiar with ParaView or VTK, you know that post-processing of the input data is organized through pipeline. Each operation can be characterized by the number of inputs and the number of outputs. A "source" or "reader" do not require inputs, but produce some outputs; a "writer"
take an or several inputs but do not produce additional data; a "filter" performs some operation to inputs and generates the results. This input / output meta-informaton is needed to initialize the class. In this case, as a generic mesh format *reader*, no inputs are required (so you do not need to select an existing object in ParaView before using this plugin to open a file), and it only returns 1 object as a `vtkUnstructuredGrid`, an unstructured mesh defined by points coordinates and cell connectivities (as meshio reads and writes).

Until now, only VTK objects are involved (`VTKPythonAlgorithmBase` is in fact defined by VTK). To declare this class as an effective *reader* usable under ParaView, it has to be decorated by ParaView functions.
``` python
from paraview.util.vtkAlgorithm import smdomain, smhint, smproperty, smproxy
@smproxy.reader(
    label="meshio Reader",
    extensions=meshio_supported_ext,  # [msh, med, inp, fem, ...]
    file_description="meshio-supported files",
)
class meshioReader(VTKPythonAlgorithmBase):
    ...
```
By doing so, the plugin will be registered as a *reader* and when you open files, the addtional file formats will be available as "meshio-supported files" in the dialog.

<img src="/assets/images/2019/10/paraview_new_inputs.png" width="795px" />

### Data generation

The mesh reading and output to ParaView pipeline is performed in the `RequestData` method of `VTKPythonAlgorithmBase`. In my case, it can be summarized as follows
``` python
from vtkmodules.numpy_interface import dataset_adapter as dsa
from vtkmodules.vtkCommonDataModel import vtkUnstructuredGrid
def RequestData(self, request, inInfo, outInfo):
    # Use meshio to read the mesh
    mesh = meshio.read(self._filename, self._file_format)

    # Produce ParaView output from mesh
    output = dsa.WrapDataObject(vtkUnstructuredGrid.GetData(outInfo))
    output.SetPoints(points)  # point coordinates
    output.SetCells(cell_types, cell_offsets, cell_conn)  # cell connectivities

    output.PointData.append(array, name)  # point data
    output.CellData.append(array, name)  # cell data
    output.FieldData.append(array, name)  # field data
```
The amazing part of this Python approach is that the `meshio` library can be directly used to do the dirtiest work (through `meshio.read`) of actually reading the mesh file. Later on we only need to carefully wrap the `mesh` object into the ParaView-desired output `outInfo`. The connection between ParaView VTK objects and pure Python is achieved by `vtkmodules.numpy_interface.dataset_adapter`. By doing
``` python
output = dsa.WrapDataObject(vtkUnstructuredGrid.GetData(outInfo))
```
The numpy-friendly object `output` can be used to construct the mesh for output. Numpy arrays can be directly used when defining node coordinates via `SetPoints`, cell connectivities via `SetCells`, etc.

### Additional GUI

Some GUI elements can be added to the plugin to provide additional parameters to the plugin. These parameters can be continuous (integers, floats) or discrete in nature (a list of choices). In this example, as suggested by one of the Github user, I added a file format (string) selector to for users to explicitly indicate the mesh format of the input file. It can be defined as additional methods inside the class
``` python
@smproperty.stringvector(name="StringInfo", information_only="1")
def GetStrings(self):
    return meshio_input_filetypes

@smproperty.stringvector(name="FileFormat", number_of_elements="1")
@smdomain.xml(
    """<StringListDomain name="list">
            <RequiredProperties>
                <Property name="StringInfo" function="StringInfo"/>
            </RequiredProperties>
        </StringListDomain>
    """
)
def SetFileFormat(self, file_format):
    ...
```
In this case, the GUI (string list) must be defined through raw XML format. In other cases (floats, integers...), simple decorators can be used, see the [documentation](https://kitware.github.io/paraview-docs/latest/python/paraview.util.vtkAlgorithm.html).

## Conclusions

The Python `VTKPythonAlgorithmBase` interface provides a powerful and easy-to-maintain approach of defining ParaView plugins. Since it is pure Python, additional technical Python libraries can be directly used to process the data. It can also be easily distributed to other users, since only one source file is involved.
