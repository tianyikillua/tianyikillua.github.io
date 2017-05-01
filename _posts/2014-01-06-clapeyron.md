---
title: Clapeyron's theorem
tags:
  - 力学
---

最近看到这个定理，其实不是第一次看到这个公式只不过知道原来这个公式叫这个名字，其实不是最近其实看到有段时间了，不过最近有点搞明白了，其实不是最近就是这几天...

在说正事之前说说夏洛克第三季，好感人啊第二集...周末把第二季补了补，原来 Sherlock 最后去救 The woman 了...当初竟然没有看出来。好了不日常了。

这个听上去有点奇怪的定理针对一个小变形分析下静态（有没有能量消耗都没关系，可以有塑性或我现在在搞的损伤）固体。为此先复习下一些小定义：一个固体 $$\Omega$$ 处于静态平衡时，对于所有虚函数 $$v$$，其位移 $$u$$ 满足

$$
\int_\Omega\sigma(u):D(v)=\int_\Omega f\cdot v
+\int_{\Gamma_F}F\cdot v+\int_{\Gamma_u}\sigma\,n\cdot v=W(v)
$$

其中 $$D(v)=(\nabla v^\mathsf{T}+\nabla v)/2$$，而 $$W$$ 代表了所有外力（包括 $$\Gamma_u$$ 上的约束力）所做的“功”。小变形分析说明有 $$\varepsilon(u)=D(u)$$，所以我们有

$$
\int_\Omega\sigma(u):\varepsilon(v)=W(v)
$$

至此 Rappels 完毕，开始 Remarques...首先前面我说的是虚函数而不是虚位移或者虚速度是为了减少一些没有必要的误解...你可以将任意你想要的东西带入 $$v$$，只要它满足一些数学上的光滑性要求，它可以是实际真实的速度场也可以是任意你自己造的一个位移场。其次我说的是“功”，因为其实...$$W$$ 这个线性泛函仅仅用来代表外力，下面将说到其实 $$W(u)$$ 本身不能代表功。

说远了，貌似还没说 Clapeyron's theorem 呢！这个定理就是说这个静态平衡的固体拥有的的弹性势能，即

$$
\mathcal{E}(u)=\frac{1}{2}\int_\Omega\sigma(u):\varepsilon(u)
$$

等于外力做“功”的**一半**，注意是一半！

其实这个定理很好证，只需要把真实的位移场 $$u$$ 带入虚功率定理得到

$$
\mathcal{E}(u)=\frac{1}{2}\int_\Omega\sigma(u):\varepsilon(u)=\frac{1}{2}W(u)
$$

这个定理对于一个弹性固体简直是一个悖论的存在...因为弹性固体是没有任何能量损耗的，那么怎么会只有一半的功转换为弹性势能呢？另外一半到哪里去了？

解决这个悖论就需要仔细重新检查看我们上面所说的“功”。对于一个静态固体没有运动哪里有功？所以这个定理背后隐含着这个固体的位移场 $$t\mapsto u(t)$$ 从零到稳态 $$u=u(T)$$ 的运动[^1]。这个运动是由外力 $$W$$ 造成了，不是我们 Imposer 了体积力 $$f$$ 或面积力 $$F$$，就是我们控制着固体表面某一部分 $$\Gamma_u$$ 的位移。让我们回顾一下热力学第一定理，即真正的能量守恒，在上述运动下，对于一个没有初应力的弹性固体它说到

$$
\mathcal{E}(u)=\int_0^T\left(\int_\Omega f\cdot\dot u
+\int_{\Gamma_F}F\cdot\dot u+\int_{\Gamma_u}\sigma\,n\cdot\dot u\right)\,\mathrm{d}t=\int_0^TW(\dot u)\,\mathrm{d}t
$$

注意到了么，实际外力做的功是其功率 $$W(\dot u)$$ 的积分！而根据乘积求导公式我们可以得到

$$
\int_0^TW(\dot u)\,\mathrm{d}t=W(u)-\int_0^T\left(\int_\Omega \dot f\cdot u
+\int_{\Gamma_F}\dot F\cdot u+\int_{\Gamma_u}\dot \sigma\,n\cdot u\right)\,\mathrm{d}t
$$

而这个减去的部分就是前面我们询问的失去的另外一半！之所以我说前面 Clapeyron's theorem 中的“功”不是真正的做功，因为它只计算了平衡状态下的外力在平衡位移场 $$u$$ 下做的“功”，而事实上外力在运动中是在变化的（否则就不会有运动...）。

举个简单的例子，一个弹性系数为 $$k$$ 的弹簧从位移零到静态位移 $$u$$ 的运动中获得了 $$ku^2/2$$ 的弹性势能，此时外力是 $$ku$$，所以 $$2\cdot ku^2/2=ku\cdot u$$ 即 Clapeyron's theorem 果然成立...但事实上外力做功应该这么计算

$$
\int_0^u kx\,\mathrm{d}x=\frac{1}{2}ku^2
$$

[^1]: 滥用记号...$$u$$ 既代表位移的时间函数又代表稳态下的位移场。