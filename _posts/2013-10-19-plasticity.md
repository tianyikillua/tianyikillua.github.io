---
title: 塑性力学
tags:
  - 力学
---

[之前的一篇文章](/2013/10/17/msg)介绍了广义标准模型 Matériaux standards généralisés 的一般框架，在这个框架中，定义一个材料的本构方程只需要定义两个函数。一个是自由势能 $$\psi$$，它引入了所有内变量及其对应的热力学力，即状态方程 Lois d'état。另外一个消耗能 $$\phi$$ 引入了所有内变量的速率并定义了所有内变量的演化方程，而且使得热力学第二定律自动满足。

这篇文章讲下一个很经典的材料模型：考虑加工硬化的塑性材料。在这个模型中我们考虑永久形变并假设随着这些塑性形变材料的弹性极限不断增加，即加工硬化。在这个模型中受力速度不影响材料的受力相应，即 Rate indenpendent。

首先引入内变量，除了应变 $$\varepsilon$$ 外还需要塑性应变 $$\varepsilon_\mathrm{p}$$ 和刻画加工硬化的参数 $$p$$。先写下自由势能，它具有如下的形式：

$$
\psi(\varepsilon,\varepsilon_\mathrm{p},p)=\frac{1}{2}\varepsilon_\mathrm{e}^\mathsf{T}C\varepsilon_\mathrm{e}+G(p)
$$

其中 $$\varepsilon_\mathrm{e}=\varepsilon-\varepsilon_\mathrm{p}$$ 为弹性形变。矩阵 $$C$$ 为广义胡克刚度矩阵，而函数 $$G$$ 描述了贮藏在材料中的塑性形变能，所以我们需要它非负、零点处为零、而且单调增即 $$G'(p)\geq 0$$。

很容易计算出塑性形变所对应的热力学力就是应力，因为

$$
A_{\varepsilon_\mathrm{p}}=-\frac{\partial\psi}{\partial\varepsilon_\mathrm{p}}=C(\varepsilon-\varepsilon_\mathrm{p})=\sigma
$$

对应参数 $$p$$ 的热力学力为 $$A_p=-\partial_p\psi=-G'(p)=R$$，它的量纲也是应力，它刻画了材料弹性区域的大小。

接下来需要定义这些内变量的演化方程，为此需要定义消耗能。事实上所有速率无关的材料的消耗能都是正齐次的，所以只需要定义一个凸的阀值函数即可，我们有：

$$
f(\sigma,R)=\sqrt{\sigma^\mathsf{T}B\sigma}+R-R_\mathrm{e}
$$

我们让函数 $$R(p)=-G'(p)\leq 0$$ 在应力空间中控制弹性区域的大小，并且让 $$R(0)=0$$ 使得材料一开始的弹性极限为 $$R_\mathrm{e}$$。函数 $$H:\sigma\mapsto H(\sigma)=\sqrt{\sigma^\mathsf{T}B\sigma}$$ 为 Hill 等效应力，当矩阵 $$B$$ 取某一个特殊形式时可以回到一般的（各项同性） Von Mises 应力。

于是消耗函数可以写成：

$$
\phi(\dot{\varepsilon}_\mathrm{p},\dot{p})=\sup_{f\leq 0}(\sigma:\dot{\varepsilon_\mathrm{p}}+R\dot{p})
$$

根据 KKT 条件，这个最大化问题等效为：

$$
\left\{
\begin{aligned}
& \dot{\varepsilon}_\mathrm{p}=\lambda\frac{\partial f}{\partial\sigma} \\
& \dot{p}=\lambda \\
& \lambda\geq 0\quad f(\sigma,R)\leq 0\quad \lambda\,f(\sigma,R)=0
\end{aligned}
\right.
$$

至此建模完成，之后就是数学分析和数值计算的事情了...这里只提一点，通过 Hill 等效应力的特殊形式，我们得到：

$$
\frac{\partial f}{\partial\sigma}=\frac{B\sigma}{H(\sigma)}
$$

所以我们得到（别忘记我们也得到了 $$\lambda=\dot{p}$$）：

$$
\dot{\varepsilon}_\mathrm{p}=\dot{p}\frac{B\sigma}{H(\sigma)}\implies\dot{p}=\sqrt{\dot{\varepsilon}_\mathrm{p}^\mathsf{T}B^{-1}\dot{\varepsilon}_\mathrm{p}}
$$

所以事实上消耗函数等于：

$$
\begin{aligned}
\phi(\dot{\varepsilon}_\mathrm{p},\dot{p}) &= \sigma:\dot{\varepsilon_\mathrm{p}}+R\dot{p} \\
&= H(\sigma)\dot{p}+R\dot{p} \\
&= \bigl(f(\sigma,R)+R_\mathrm{e}\bigr)\dot{p} \\
&= R_\mathrm{e}\dot{p}\geq 0
\end{aligned}
$$
