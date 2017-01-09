---
title: Intégration de Lebesgue et distribution
categories:
  - 数学
---

...先插一条日志讲讲 Lebesgue 积分和广义函数（也叫分布，但和概率中的分布函数完全不是同一个东西）。Lebesgue 积分是我们常见的 Riemann 积分的推广，因为我们发现了很多函数 Riemann 不可积，比如...

$$
f(x)=\begin{cases}1 & x\in\mathbb{R}\cap[0,1] \\ 0 & x\in\mathbb{Q}\cap[0,1]\end{cases}
$$

但这个函数却是 Lebesgue 可积的，所以 Lebesgue 积分体系就扩大了可积函数的空间，并事实上将其变成了一个 Banach 空间（完备存在范数的无限维线性空间）。比如说上面那个函数我们有...

$$
\int_\mathbb{R}f(x)\,\mathrm{d}x=1
$$

因为几乎处处（Presque partout）这个函数在 $$[0,1]$$ 上等于常值函数 $$x\mapsto 1$$，因为有理数集是可数的所以它的测度为0。恩的确，Lebesgue 积分是建立在测度理论之上的，对积分的概念进行了超级强大的推广，没有说只能在实数域或复数域上对函数进行积分，只要这个函数联系着两个可测集合（Ensemble mesurable）且这个函数本身也是可测的，那么就可以定义积分。下面讲讲分布，我们的动机是如下这个“函数”...

$$\delta(x)=0$$ 对于所有 $$\mathbb{R}\ni x\neq 0$$，而且有...

$$
\int_\mathbb{R}\delta(x)\,\mathrm{d}x=1
$$

由于根据 Lebesgue 积分，这个函数几乎处处等于常值函数 $$x\mapsto 0$$，所以它的积分必然为0，所以这种函数不存在。但在物理上，这个函数非常有用，称作单位脉冲“函数”，那如何给它一个严密的定义呢？考虑下面的函数数列 $$\delta_n:\mathbb{R}\to\mathbb{R}$$

$$
\delta_n(x)=\begin{cases} n & |x|<\frac{1}{2n} \\ 0 & \text{sinon}\end{cases}
$$

可以看到如果 $$n\to+\infty$$，这个函数数列越来越接近我们所说的一个单位脉冲（积分为1），但根据上面所说，这个函数数列不收敛，因为不存在极限。所以我们想建立这么一个体系，在这个体系下上面的这个数列能够收敛到这个体系下的单位脉冲。所以下面要做的是...

1. 建立这个体系
2. 定义到底什么是单位脉冲
3. 看是不是上面那个数列能够“收敛”到单位脉冲

Laurent Schawarz 建立的分布理论很好地回答了这个问题～让我想想怎么讲，貌似有点小复杂了。他先建立了一类“测试函数”空间 $$\mathcal{D}$$，这类函数性质很好，意思就是无限可导而且在某个区间之外这个函数就一定为0。然后它就定义所谓的分布（Distribution）或广义函数就是在这个函数空间上的线性型，即 $$\phi:\mathcal{D}\to\mathbb{C}$$，即对于广义函数而言它输入一个测试函数，吐出一个复数。那么这个广义函数如何和一般的函数获得联系呢？设 $$f:\mathbb{R}\to\mathbb{C}$$ 一个函数，那么我们设 $$f$$ 所代表的分布 $$T_f$$，如果存在的话，定义为...

$$
T_f(\phi)=\int_\mathbb{R}f(x)\phi(x)\,\mathrm{d}x
$$

通过 Lebesgue 积分，可以证明只要 $$f\in L^1_\mathrm{loc}$$ 即只要函数[局部可积](http://en.wikipedia.org/wiki/Locally_integrable_function)，那么这个积分就存在，也就说存在着 $$f$$ 所对应的分布。反过来，如果存在一个分布由上面的公式所定义，也可以反过来找到原来的函数 $$f$$（事实上得加上几乎处处的条件），也就是说存在 $$f\leftrightarrow T_f$$ 之间的一个一一对应。所以分布是局部可积函数的一个推广。若 $$T$$ 为一个分布，之后我们记 $$\langle T,\phi\rangle=T(\phi)$$。然后就来正事了，我们定义单位脉冲分布为...

$$
\langle\delta,\phi\rangle=\phi(0)
$$

并定义一个分布数列 $$T_n$$ 收敛到一个分布 $$T$$的条件是有...

$$
\lim_{n\to+\infty}\langle T_n,\phi\rangle=\langle T,\phi \rangle
$$

对于所有的测试函数。下面我们看看上面所定义的数列 $$\delta_n$$ 在分布的理论下是不是收敛。$$\delta_n$$ 作为一个分布，定义为...

$$
\langle\delta_n,\phi\rangle=\int_{-1/2n}^{1/2n}n\phi(x)\,\mathrm{d}x
$$

当 $$n\to+\infty$$ 时，我们有...

$$
\lim\int_{-1/2n}^{1/2n}n\phi(x)\,\mathrm{d}x=\lim n\left(\frac{1}{2n}+\frac{1}{2n}\right)\phi\bigl(\theta(n)\bigr)
$$

其中 $$\lvert\theta(n)\rvert<1/2n$$，根据均值定理。由于 $$\phi$$ 连续，所以得到...

$$
\lim_{n\to+\infty}n\left(\frac{1}{2n}+\frac{1}{2n}\right)\phi\bigl(\theta(n)\bigr)=\phi(0)
$$

所以...

$$
\lim_{n\to+\infty}\langle\delta_n,\phi\rangle=\phi(0)
$$

而这个恰好是 $$\delta$$ 的定义！所以我们得到上面的数列在分布理论下收敛到单位脉冲，事实上分布理论还可以使得[单位阶跃函数](http://en.wikipedia.org/wiki/Heaviside_step_function)的导数为单位脉冲，这个很直观吧，但不靠分布理论是不行嘀...说了好多。