---
title: 计算力学中各种张量的表达
tags:
  - 力学
  - 张量
  - 物理
  - 数学
words_per_minute: 120
---

固体力学涉及了各种各样的张量，比如应力、应变、弹性张量等等。在数值仿真中，根据约定不同，它们具有很多不同的矩阵表达式。这篇博文旨在帮助计算力学工作者梳理一些基本的张量表达知识。

## 二阶张量及其表达

固体力学中常见的二阶张量有应变 $$\boldsymbol{\varepsilon}$$ 和应力 $$\boldsymbol{\sigma}$$。在小变形假设下，它们均为二阶对称张量

$$
\newcommand{\stress}{\boldsymbol{\sigma}}
\newcommand{\strain}{\boldsymbol{\varepsilon}}
\strain=\begin{bmatrix}
\varepsilon_{11} & \varepsilon_{12} & \varepsilon_{13} \\
\varepsilon_{12} & \varepsilon_{22} & \varepsilon_{23} \\
\varepsilon_{13} & \varepsilon_{23} & \varepsilon_{33} \\
\end{bmatrix},\quad \stress=\begin{bmatrix}
\sigma_{11} & \sigma_{12} & \sigma_{13} \\
\sigma_{12} & \sigma_{22} & \sigma_{23} \\
\sigma_{13} & \sigma_{23} & \sigma_{33} \\
\end{bmatrix}
$$

对于这类张量，至少存在以下三种表达方式。

- 应用于应变的 Voigt 记号

$$
\strain_\mathrm{V}=\begin{bmatrix}
\varepsilon_{11} \\ \varepsilon_{22} \\ \varepsilon_{33} \\ 2\varepsilon_{12} \\ 2\varepsilon_{13} \\ 2\varepsilon_{23}
\end{bmatrix}
$$

- 应用于应力的 Voigt 记号

$$
\stress_\mathrm{V}=\begin{bmatrix}
\sigma_{11} \\ \sigma_{22} \\ \sigma_{33} \\ \sigma_{12} \\ \sigma_{13} \\ \sigma_{23}
\end{bmatrix}
$$

- Mandel 记号，可以应用于任意二阶对称张量

$$
\strain_\mathrm{M}=\begin{bmatrix}
\varepsilon_{11} \\ \varepsilon_{22} \\ \varepsilon_{33} \\ \sqrt{2}\varepsilon_{12} \\ \sqrt{2}\varepsilon_{13} \\ \sqrt{2}\varepsilon_{23}
\end{bmatrix}
$$

这三种记号都满足如下内积守恒

$$
\strain\cdot\stress=\sum_{i=1}^3\sum_{j=1}^3\varepsilon_{ij}\sigma_{ij}=\strain_\mathrm{V}\cdot\stress_\mathrm{V}=\strain_\mathrm{M}\cdot\stress_\mathrm{M}
$$

其中 $$\strain\cdot\stress$$ 中的内积理解成二阶张量之间的 double contraction，而 Voigt 记号 和 Mandel 记号中的内积理解成 $$\mathbb{R}^6$$ 中的内积 $$\mathbf{u}\cdot\mathbf{v}=\sum_{i=1}^6 u_iv_i$$。内积守恒条件使得我们可以用普通矢量之间的内积来计算二阶张量的内积。由于 $$\strain\cdot\stress$$ 项经常出现于固体力学的弱形式中，所以该条件非常有用。

商业计算力学软件中普遍使用 Voigt 记号（比如 [Abaqus](https://help.3ds.com/2023/English/DSSIMULIA_Established/SIMACAEMODRefMap/simamod-c-conventions.htm?contextscope=all&id=274ceb5c39b8484a8afbce41676a635e#simamod-c-conventions-t-StressAndStrainMeasures-sma-topic20)），主要有如下原因

- 在应用于应变的 Voigt 记号中，剪切部分 $$(2\varepsilon_{12}, 2\varepsilon_{13}, 2\varepsilon_{23})$$ 可以直接理解成工程剪切应变。对于应力，$$(\sigma_{12}, \sigma_{13}, \sigma_{23})$$ 直接就可以理解成剪切应力。
- “工程师”可能无法理解 Mandel 记号中出现的 $$\sqrt{2}$$ 项

但同时，由于对于应力和应变的处理不同，Voigt 记号对于计算力学软件开发不是很友好。一些研究导向的计算力学软件（比如 [MFront](https://tfel.sourceforge.net/tensors.html)）经常使用 Mandel 记号。

在这三种记号中，对于剪切部分的顺序也存在很多约定。[Abaqus](https://help.3ds.com/2023/English/DSSIMULIA_Established/SIMACAEMODRefMap/simamod-c-conventions.htm?contextscope=all&id=274ceb5c39b8484a8afbce41676a635e#simamod-c-conventions-t-StressAndStrainMeasures-sma-topic20) 和 [MFront](https://tfel.sourceforge.net/tensors.html) 使用 $$(11, 22, 33, 12, 13, 23)$$，但 [ANSYS](http://dl.mycivil.ir/reza/ans_thry.pdf) 使用 $$(11, 22, 33, 12, 23, 13)$$。这个只是约定，每个人可以有自己的偏好。由于本人工作有时候需要和 Abaqus 打交道，所以个人偏好 $$(11, 22, 33, 12, 13, 23)$$。

在大变形假设下，固体力学中还存在很多非对称二阶张量，比如 deformation gradient

$$
\mathbf{F}=\begin{bmatrix}
F_{11} & F_{12} & F_{13} \\
F_{21} & F_{22} & F_{23} \\
F_{31} & F_{32} & F_{33} \\
\end{bmatrix}
$$

[MFront](https://tfel.sourceforge.net/tensors.html) 采取的是如下记号

$$
\mathbf{F}_\mathrm{M}=(F_{11}, F_{22}, F_{33}, F_{12}, F_{21}, F_{13}, F_{31}, F_{23}, F_{32})
$$

## 四阶张量及其表达

在分别选取线性空间 $$V$$ 和 $$W$$ 的一个基底之后，一个线性映射 $$T:V\to W$$ 可以由一个矩阵表示

$$
T(\mathbf{v}_j)=\sum_{i=1}^m T_{ij}\mathbf{w}_i\quad\implies T=\begin{bmatrix}
T_{11} & T_{12} & \ldots & T_{1n} \\
T_{21} & T_{22} & \ldots & T_{2n} \\
\ldots & \ldots & \ldots & \ldots \\
T_{m1} & T_{m2} & \ldots & T_{mn} \\
\end{bmatrix}
$$

其中 $$(\mathbf{v}_1, \mathbf{v}_2, \ldots, \mathbf{v}_n)$$ 为 $$n$$ 维线性空间 $$V$$ 的基底，$$(\mathbf{w}_1, \mathbf{w}_2, \ldots, \mathbf{w}_m)$$ 为 $$m$$ 维线性空间 $$W$$ 的基底。

### 弹性张量

固体力学中的四阶张量经常理解成从二阶张量到二阶张量的一个线性映射，比如弹性张量 $$\mathbb{C}$$ 就是一个从应变到应力的映射

$$
\mathbb{C}:\strain\mapsto\stress=\mathbb{C}\strain\quad\iff\quad\stress_{ij}=\sum_{k=1}^3\sum_{l=1}^3\mathbb{C}_{ijkl}\strain_{kl}
$$

由于应力、应变的对称性，我们得到 minor symmetry，即 $$\mathbb{C}_{ijkl}=\mathbb{C}_{jikl}=\mathbb{C}_{ijlk}$$。由于弹性张量通常由一个 elastic energy potential 二阶求导获得，所以还满足 major symmetry，即 $$\mathbb{C}_{ijkl}=\mathbb{C}_{klij}$$。

之前所介绍的 Voigt 记号和 Mandel 记号其实均为二阶对称张量集合的一个基底。根据基底的选择不同，
弹性张量 $$\mathbb{C}$$ 也有不用的矩阵表现。需要注意的是 Voigt 记号其实涵盖了两个基底的选择：定义域为应变，使用对应于应变的记号；值域为应力，使用对应于应力的记号。在 Voigt 记号下，我们得到

$$
\begin{bmatrix}
\sigma_{11} \\ \sigma_{22} \\ \sigma_{33} \\ \sigma_{12} \\ \sigma_{13} \\ \sigma_{23}
\end{bmatrix}=
\begin{bmatrix}
C_{0000} & C_{0011} & C_{0022} & C_{0001} & C_{0002} & C_{0012} \\
{C}_{0011} & C_{1111} & C_{1122} & C_{1101} & C_{1102} & C_{1112} \\
{C}_{0022} & C_{1122} & C_{2222} & C_{2201} & C_{2202} & C_{2212} \\
{C}_{0001} & C_{1101} & C_{2201} & C_{0101} & C_{0102} & C_{0112} \\
{C}_{0002} & C_{1102} & C_{2202} & C_{0102} & C_{0202} & C_{0212} \\
{C}_{0012} & C_{1112} & C_{2212} & C_{0112} & C_{0212} & C_{1212}
\end{bmatrix}\begin{bmatrix}
\varepsilon_{11} \\ \varepsilon_{22} \\ \varepsilon_{33} \\ 2\varepsilon_{12} \\ 2\varepsilon_{13} \\ 2\varepsilon_{23}
\end{bmatrix}
$$

这里的 $$C_{ijkl}$$ 的角标采取以 0 为基准的编号。

如果使用 Mandel 记号，我们有

$$
\begin{bmatrix}
\sigma_{11} \\ \sigma_{22} \\ \sigma_{33} \\ \sqrt{2}\sigma_{12} \\ \sqrt{2}\sigma_{13} \\ \sqrt{2}\sigma_{23}
\end{bmatrix}=
\begin{bmatrix}C_{0000} & C_{0011} & C_{0022} & \sqrt{2} C_{0001} & \sqrt{2} C_{0002} & \sqrt{2} C_{0012}\\C_{0011} & C_{1111} & C_{1122} & \sqrt{2} C_{1101} & \sqrt{2} C_{1102} & \sqrt{2} C_{1112}\\C_{0022} & C_{1122} & C_{2222} & \sqrt{2} C_{2201} & \sqrt{2} C_{2202} & \sqrt{2} C_{2212}\\\sqrt{2} C_{0001} & \sqrt{2} C_{1101} & \sqrt{2} C_{2201} & 2 C_{0101} & 2 C_{0102} & 2 C_{0112}\\\sqrt{2} C_{0002} & \sqrt{2} C_{1102} & \sqrt{2} C_{2202} & 2 C_{0102} & 2 C_{0202} & 2 C_{0212}\\\sqrt{2} C_{0012} & \sqrt{2} C_{1112} & \sqrt{2} C_{2212} & 2 C_{0112} & 2 C_{0212} & 2 C_{1212}\end{bmatrix}\begin{bmatrix}
\varepsilon_{11} \\ \varepsilon_{22} \\ \varepsilon_{33} \\ \sqrt{2}\varepsilon_{12} \\ \sqrt{2}\varepsilon_{13} \\ \sqrt{2}\varepsilon_{23}
\end{bmatrix}
$$

对于各向同性的线性弹性理论，弹性张量可以由两个拉梅系数表示

$$
\stress=\mathbb{C}\strain=\lambda\cdot\mathrm{tr}(\strain)\cdot\mathbb{I}_3+2\mu\strain
$$

可以简单验证 $$\mathbb{C}$$ 的确是一个从 $$\strain$$ 到 $$\stress$$ 的线性映射。在这个情况下，它的 Voigt 记号和 Mandel 记号分别得到

$$
\mathbb{C}_\mathrm{V}=\begin{bmatrix}\lambda + 2 \mu & \lambda & \lambda & 0 & 0 & 0\\\lambda & \lambda + 2 \mu & \lambda & 0 & 0 & 0\\\lambda & \lambda & \lambda + 2 \mu & 0 & 0 & 0\\0 & 0 & 0 & \mu & 0 & 0\\0 & 0 & 0 & 0 & \mu & 0\\0 & 0 & 0 & 0 & 0 & \mu\end{bmatrix} \\
\mathbb{C}_\mathrm{M}=\begin{bmatrix}\lambda + 2 \mu & \lambda & \lambda & 0 & 0 & 0\\\lambda & \lambda + 2 \mu & \lambda & 0 & 0 & 0\\\lambda & \lambda & \lambda + 2 \mu & 0 & 0 & 0\\0 & 0 & 0 & 2\mu & 0 & 0\\0 & 0 & 0 & 0 & 2\mu & 0\\0 & 0 & 0 & 0 & 0 & 2\mu\end{bmatrix}
$$

### 张量的旋转

张量之所以为张量而不是矩阵，关键就在于它本质上并不取决于基底、即坐标系的选择。一个坐标系的转变将对应于张量的矩阵表达式的转变。

在 $$\mathbb{R}^3$$ 中考虑一个基底旋转。假设矢量 $$\mathbf{v}$$ 在新基底 $$\mathbf{e}_i'$$ 下的矩阵表达为

$$
\mathbf{v}'=\mathbf{R}^\mathsf{T}\mathbf{v}
$$

其中 $$\mathbf{R}$$ 为一个 $$3\times 3$$ 的旋转矩阵，$$\mathbf{v}$$ 为矢量在原基底下的矩阵表达（这里滥用记号）。那么对于 $$\mathbb{R}^3$$ 中的二阶张量，我们自然获得

$$
\stress'=\mathbf{R}^\mathsf{T}\stress\mathbf{R}
$$

我们可以把上述公式用一个从二阶张量到二阶张量的线性映射表示

$$
\stress'=\mathsf{R}\stress
$$

即四阶张量 $$\mathsf{R}$$ 作用在原二阶张量的矩阵表达上，得到该二阶张量在新基底下的矩阵表达。该四阶张量可以通过之前的 Voigt 或者 Mandel 记号来表达。在 Mandel 记号下，我们有

$$
\mathsf{R}_\mathrm{M}=\begin{bmatrix}R_{00}^{2} & R_{10}^{2} & R_{20}^{2} & \sqrt{2} R_{00} R_{10} & \sqrt{2} R_{00} R_{20} & \sqrt{2} R_{10} R_{20}\\R_{01}^{2} & R_{11}^{2} & R_{21}^{2} & \sqrt{2} R_{01} R_{11} & \sqrt{2} R_{01} R_{21} & \sqrt{2} R_{11} R_{21}\\R_{02}^{2} & R_{12}^{2} & R_{22}^{2} & \sqrt{2} R_{02} R_{12} & \sqrt{2} R_{02} R_{22} & \sqrt{2} R_{12} R_{22}\\\sqrt{2} R_{00} R_{01} & \sqrt{2} R_{10} R_{11} & \sqrt{2} R_{20} R_{21} & R_{00} R_{11} + R_{01} R_{10} & R_{00} R_{21} + R_{01} R_{20} & R_{10} R_{21} + R_{11} R_{20}\\\sqrt{2} R_{00} R_{02} & \sqrt{2} R_{10} R_{12} & \sqrt{2} R_{20} R_{22} & R_{00} R_{12} + R_{02} R_{10} & R_{00} R_{22} + R_{02} R_{20} & R_{10} R_{22} + R_{12} R_{20}\\\sqrt{2} R_{01} R_{02} & \sqrt{2} R_{11} R_{12} & \sqrt{2} R_{21} R_{22} & R_{01} R_{12} + R_{02} R_{11} & R_{01} R_{22} + R_{02} R_{21} & R_{11} R_{22} + R_{12} R_{21}\end{bmatrix}
$$

通过该矩阵表达，当我们想计算任意二阶对称张量 $$\strain$$ 的基底变化时，我们需要做的是

1. 将该二阶张量表达在 Mandel 记号下，获得 $$\strain_\mathrm{M}$$
2. 进行矩阵乘法运算 $$\mathsf{R}_\mathrm{M}\strain_\mathrm{M}$$，获得 $$\strain'_\mathrm{M}$$

### Acoustic tensor

在计算力学中，给定一个弹性张量 $$\mathbb{C}$$ 和一个 $$\mathbb{R}^3$$ 中的单位向量 $$\mathbf{n}$$，我们可以计算如下定义的二阶对称张量 acoustic tensor

$$
A_{ik}=\sum_{j=1}^3\sum_{l=1}^3 n_j\cdot C_{ijkl}\cdot n_l
$$

该张量 $$\mathbf{A}$$ 在波动方程和稳定性问题中有相关应用。

同样，我们可以认为 $$\mathbf{A}$$ 是一个四阶张量 $$\mathbb{A}$$ 作用在二阶张量 $$\mathbf{n}\otimes\mathbf{n}$$ 上所得到。将 $$\mathbf{A}$$ 与 $$\mathbf{n}\otimes\mathbf{n}$$ 表达在 Mandel 记号下，那么 $$\mathbb{A}$$ 的矩阵表达为

$$
\mathbb{A}_\mathrm{M}=\begin{bmatrix}C_{00} & \frac{C_{33}}{2} & \frac{C_{44}}{2} & C_{03} & C_{04} & \frac{\sqrt{2} C_{34}}{2}\\\frac{C_{33}}{2} & C_{11} & \frac{C_{55}}{2} & C_{13} & \frac{\sqrt{2} C_{35}}{2} & C_{15}\\\frac{C_{44}}{2} & \frac{C_{55}}{2} & C_{22} & \frac{\sqrt{2} C_{45}}{2} & C_{24} & C_{25}\\C_{03} & C_{13} & \frac{\sqrt{2} C_{45}}{2} & C_{01} + \frac{C_{33}}{2} & \frac{\sqrt{2} C_{05}}{2} + \frac{C_{34}}{2} & \frac{\sqrt{2} C_{14}}{2} + \frac{C_{35}}{2}\\C_{04} & \frac{\sqrt{2} C_{35}}{2} & C_{24} & \frac{\sqrt{2} C_{05}}{2} + \frac{C_{34}}{2} & C_{02} + \frac{C_{44}}{2} & \frac{\sqrt{2} C_{23}}{2} + \frac{C_{45}}{2}\\\frac{\sqrt{2} C_{34}}{2} & C_{15} & C_{25} & \frac{\sqrt{2} C_{14}}{2} + \frac{C_{35}}{2} & \frac{\sqrt{2} C_{23}}{2} + \frac{C_{45}}{2} & C_{12} + \frac{C_{55}}{2}\end{bmatrix}
$$

其中 $$C_{ij}$$ 为弹性张量在 Mandel 记号下的矩阵表达。

在各向同性线性弹性理论下，我们得到

$$
\mathbb{A}_\mathrm{M}=\begin{bmatrix}\lambda + 2 \mu & \mu & \mu & 0 & 0 & 0\\\mu & \lambda + 2 \mu & \mu & 0 & 0 & 0\\\mu & \mu & \lambda + 2 \mu & 0 & 0 & 0\\0 & 0 & 0 & \lambda + \mu & 0 & 0\\0 & 0 & 0 & 0 & \lambda + \mu & 0\\0 & 0 & 0 & 0 & 0 & \lambda + \mu\end{bmatrix}
$$

所以对于 acoustic tensor，我们有

$$
\mathbf{A}_\mathrm{M}=\begin{bmatrix}\lambda + 2 \mu & \mu & \mu & 0 & 0 & 0\\\mu & \lambda + 2 \mu & \mu & 0 & 0 & 0\\\mu & \mu & \lambda + 2 \mu & 0 & 0 & 0\\0 & 0 & 0 & \lambda + \mu & 0 & 0\\0 & 0 & 0 & 0 & \lambda + \mu & 0\\0 & 0 & 0 & 0 & 0 & \lambda + \mu\end{bmatrix}
\begin{bmatrix}n_{0}^{2}\\n_{1}^{2}\\n_{2}^{2}\\\sqrt{2} n_{0} n_{1}\\\sqrt{2} n_{0} n_{2}\\\sqrt{2} n_{1} n_{2}\end{bmatrix} \\
=\begin{bmatrix}\mu {n}_{1}^{2} + \mu {n}_{2}^{2} + \left(\lambda + 2 \mu\right) {n}_{0}^{2}\\\mu {n}_{0}^{2} + \mu {n}_{2}^{2} + \left(\lambda + 2 \mu\right) {n}_{1}^{2}\\\mu {n}_{0}^{2} + \mu {n}_{1}^{2} + \left(\lambda + 2 \mu\right) {n}_{2}^{2}\\\sqrt{2} \left(\lambda + \mu\right) {n}_{0} {n}_{1}\\\sqrt{2} \left(\lambda + \mu\right) {n}_{0} {n}_{2}\\\sqrt{2} \left(\lambda + \mu\right) {n}_{1} {n}_{2}\end{bmatrix}
$$

## Python 库

为方便获取上述张量的矩阵表达，我开发了一个基于 [sympy](https://www.sympy.org/en/index.html) 的 Python 库。由于是在工作期间开发，所以我先得确认一下是不是可以开源……

- 支持二阶和四阶张量的表达
- 空间可以是二维或三维
- 支持 Voigt 和 Mandel 记号

API 参考了 [`scipy.spatial.transform.Rotation`](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.transform.Rotation.html)

- `Tensor().from_...` 用某记号生成一个张量，返回张量类
- `Tensor().as_...` 用某记号表示一个张量，返回 `sympy` 矩阵

一旦可以开源的话我会更新链接分享。
