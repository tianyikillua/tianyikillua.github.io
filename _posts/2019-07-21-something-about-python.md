---
title: Python 库项目模版及 PyPI 打包
tags:
  - Python
---

最近在 Github 上一直关注的一个大神分享了 Python 库项目的模版 [pyfoobar](https://github.com/nschloe/pyfoobar)，学习了很多软件工程里面的方式和 Python 库打包，上传到 [PyPI](https://pypi.org) 上的方法，这里稍微分享一下。

官方的 Packaging 指导在[这里](https://packaging.python.org/tutorials/packaging-projects)，写得也很实用。

### 关于库文件结构

命名的话当然最好库名称（即从 PyPI 上下载的名称）和 `import` 名称一模一样，比如数值线性代数库 `numpy` 可以通过
```
pip install numpy
```
从 PyPI 上下载，然后通过
```
import numpy as np
```
的方式导入。当然如果库名称是两个甚至多个（还是算了吧）单词的合并，那么要么库名称和导入名称都用下划线 `_` 分割（因为 Python 导入名称不可以用 `-` 分割），比如 `beautiful_library`；要么两个名称不一致，一个有名的例子就是机器学习库 `scikit-learn`，其库名称就是这个，通过 `pip install scikit-learn` 下载。而其导入名称为 `sklearn`，需要告知使用者。

库名称就在最关键的 `setup.py` 中通过 `setuptools` 库的 `setup` 函数标明。通过这个文件使用者可以通过
```
python setup.py build/install [--user]
```
或者
```
pip install [-e] .
```
的方式编译/安装这个 Python 库。下面就来看看这个文件。

### 关于 `setup.py`

下面就来看看 [pyfoobar](https://github.com/nschloe/pyfoobar) 分享的 `setup.py`。
``` python
setup(
    name="pyfoobar",
    version=about["__version__"],
    packages=find_packages(),
    url="https://github.com/nschloe/pyfoobar",
    author=about["__author__"],
    author_email=about["__email__"],
    install_requires=[],
    description="A little bit of foobar in your life",
    long_description=read("README.md"),
    long_description_content_type="text/markdown",
    license=about["__license__"],
    classifiers=[
        about["__license__"],
        about["__status__"],
        # See <https://pypi.org/classifiers/> for all classifiers.
        "Operating System :: OS Independent",
        "Programming Language :: Python",
        "Programming Language :: Python :: 3",
        "Topic :: Scientific/Engineering",
        "Topic :: Scientific/Engineering :: Mathematics",
    ],
    entry_points={"console_scripts": ["pyfoobar-show = pyfoobar.cli:show"]},
)
```

几个关键的参数可以看到是
- `name`：库名称
- `version`：库的版本
- `packages`：库文件。这里用了 `setuptools` 中的 `find_packages` 函数，下面会说到。
- `install_requires`：使用这个库（必须）所需要的其他库。安装这个库的同时会检查并安装这些必需的 dependencies。
- `classifiers`：一些关于这个库的信息：版权、主题、使用的编程语言等等

如果你的库只能在特定的版本下运行，除了可以通过 `Programming Language` 的方式告知使用者，还可以通过 `python_requires` 参数强制只能安装在这些版本下，详见[这里](https://packaging.python.org/guides/distributing-packages-using-setuptools/#python-requires)。

这个模版库中把一些最关键的 metadata 都储存在了 ``__about__.py`` 文件中，比如作者、版本、版权等等，方便使用者查看这些信息。

关于版本的选择，推荐 [PEP 440](https://www.python.org/dev/peps/pep-0440) 和 [Semantic Versioning](https://semver.org)，大致就是
```
MAJOR.MINOR.PATCH
```

的版本格式。
- 如果你修补了一些  bug，那么添加 `PATCH` 的数字
- 如果你添加了一些不需要使用者修改之前函数/库 API 的功能，那么添加 `MINOR` 的数字
- 如果你添加了一些功能，并做了一些 API 的修改，使得使用者需要修改他们（使用你的库）的文件，那么添加 `MAJOR` 的数字。

可以看到这个模版中默认一开始的版本是 `0.0.1`。由于一开始 API 和功能增减特别快，我个人的方式是一开始不管修改有多大，每次就添加 `PATCH` 的数字。从 `0.1.0` 开始，按照上面的规则。

### 导入文件夹

在这个例子中，导入文件夹名称和库名称一致，都为 `pyfoobar`。在这个文件夹下有个关键的 `__init__.py` 文件，使得这个文件夹就是一个库，可以通过 `import pyfoobar` 的方式导入。
``` python
from .__about__ import __author__, __email__, __license__, __status__, __version__
from .cli import show
from .main import solve

__all__ = [
    "__author__",
    "__email__",
    "__license__",
    "__version__",
    "__status__",
    "solve",
    "show",
]
```

在运行 `import pyfoobar` 的时候所发生的事情就通过这个文件来实现，比如这里就导入 `__about__.py` 中所定义的一些 metadata 到库的 namespace 中，而库的 namespace 就通过 `__all__` 变量来说明。在导入库之后（比如 `import pyfoobar`），那么在 `dir(pyfoobar)` 之下就只会有这里所定义的变量、函数或类，比如
``` python
pyfoobar.__version__
```

就会得到库的版本。同理，如果你很懒惰地导入所有 `from pyfoobar import *` （强烈不建议，因为会导致各个库之间 namespace 冲突），那么你就只会得到这里所定义的东西。

除了 `__init__.py`，其他类似的文件还有比如 `__main__.py`。这个文件将会在你 `python3 pyfoobar` 的时候运行，即类似这个库的主程序，适合一些 GUI 库。

之前说到 `setup.py` 中的 `find_packages` 函数，事实上它就会根据一些[算法](https://setuptools.readthedocs.io/en/latest/setuptools.html#using-find-packages)包装你库中的源文件，其中一个很关键的判别方法就是看这个文件夹是否含有 `__init__.py` 文件。

### 关于发布你的 Python 库到 PyPI 上

现在通用和提倡安装 Python 库的方式就是通过 `pip`，默认从 [Python Package Index](https://pypi.org) (PyPI) 上寻找、下载之后安装你所需要的库。

要将你的库上传上 PyPI 上，使得其他人可以通过 `pip install` 的方式很方便地获得你写的库，需要先对你的库进行打包，大致就是下面这两个命令，参考 [pyfoobar](https://github.com/nschloe/pyfoobar) 分享的 `Makefile`[^1]
```
python3 setup.py sdist
python3 setup.py bdist_wheel
```

第一个命令就对库的源文件进行压缩打包，生成一个 `tar.gz` 文件。第二个命令主要针对一些包装和 interface 其他编译语言（比如 C、Fortran）的 Python 库。为了方便使用者不用再次编译那些文件，你自己先生成一个编译好的 binary wheel，然后再上传。最终上传，就通过[官方指导](https://packaging.python.org/tutorials/packaging-projects)中所说的，先注册，然后通过 `twine` 库上传。

回到上面说的一些含编译语言的库和生成 binary wheels。由于操作系统类型特别多（特别是泛 Linux 类型的 distributions），所以为了使得生成的 wheels 可以更通用，不用针对每个 distribution (Ubuntu, CentOS 和好多它们的版本等等）生成各自的 wheel，制定了 `manylinux` 标签，比如现在最新的 [manylinux2010](https://www.python.org/dev/peps/pep-0571)。

编译好的 `bdist_wheel` 要满足 `manylinux` 标签，最关键的就是其中含的编译好的库只能 link 到所制定的一些很通用的 libraries，详见[这里](https://www.python.org/dev/peps/pep-0571/#the-manylinux2010-policy)。通过这个白名单，保证编译好的库可以在很多泛 Linux 版本下使用。

在实际操作上，可以使用官方提供的 [quay.io/pypa/manylinux2010_x86_64](https://github.com/pypa/manylinux) Docker images。在这个 container 之下对你的库进行包装，保证编译好的库的通用性，可以看我的一个[例子](https://github.com/tianyikillua/medcoupling/blob/master/.travis.yml)，和 travis 结合，让服务器自动帮我编译。

### 最终推荐一个 Makefile 的替代

`Makefile` 虽然比较通用（Windows 下用起来还是比较麻烦），但是并不非常 pythonic，所以这里推荐下 [invoke](https://github.com/pyinvoke/invoke)。通过一个 `tasks.py` 文件，把一些可以自动化的命令用 Python 语言进行描述。比如上传新的库版本，先在 `__about__.py` 中修改，然后用下面的定义
``` python
from invoke import task
import pyfoobar

VERSION = pyfoobar.__version__


@task
def tag(c):
    print(f"Tagging v{VERSION}...")
    c.run(f"git tag v{VERSION}")
    c.run("git push --tags")
```
使得你可以通过 `invoke tag` 直接添加并上传新的库版本。可以看到通过一个纯 Python 文件，版本就直接通过一个使用者的角度来导入并查看（`pyfoobar.__version__`），然后最终仍然可以用 shell 运行 `git` 来运行命令。

[^1]: 下面那个生成 wheel 的命令其实不用加 `--universal` 了，因为 Python 2 剩下的时间不多了！