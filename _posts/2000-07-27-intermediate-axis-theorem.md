---
title: 一个力学小知识
tags:
  - 力学
words_per_minute: 10
header:
  video:
    id: l51LcwHOW7s
    provider: youtube
---

## 现象

这篇博文介绍一个日常生活中可以简单验证的力学小知识，叫做 [Intermediate axis theorem](https://en.wikipedia.org/wiki/Tennis_racket_theorem)。设某刚体的惯性主轴为 $$(\mathbf{e}_1, \mathbf{e}_2, \mathbf{e}_3)$$，相对应的转动惯量为 $$I_1\geq I_2\geq I_3$$。这个定理说，在没有外力矩的情况下，刚体关于第二主轴 $$\mathbf{e}_2$$ 的自转是不稳定的。

这个定理其实很好用实验证明，拿出各位的手机就行了[^1]。见下图，围绕着手机的中心，可以有三种旋转方式。

1. 围绕着 $$\mathbf{e}_1$$，在手机屏幕的平面中旋转。
2. 围绕着 $$\mathbf{e}_2$$，手机的上半部分和下半部分线速度相反。
3. 围绕着 $$\mathbf{e}_3$$，手机的左半部分和右半部分线速度相反。

<img src="/assets/images/2021/07/book.png" width="150px" />

为了去除施加在手机上的外力矩，你可以在给予初始旋转角速度的同时，把手机往上抛。手机在上升和下降过程中，尽管有重力作用，但不会收到外力矩。

通过数值模拟，我得到了如下仿真结果，从左到右分别对应上述三种旋转方式。

1. 第一种情况手机的自转是**稳定**的：手机在平面中的旋转是匀速，而且旋转轴本身几乎没有任何变化。
2. 第二种自转是**不稳定**的：手机没有一个固定的旋转方式，围绕着其他轴的旋转也参与了进来。
3. 第三种自转是**稳定**的：尽管肉眼可见旋转轴本身有稍许的变化，但主旋转仍然是围绕着初始的 $$\mathbf{e}_3$$ 轴。

<img src="/assets/images/2021/07/omega.gif" width="800px" />

如果实在不想弄坏自己的手机或者书的话，也可以看看[最上面那个 YouTube 视频](https://www.youtube.com/watch?v=l51LcwHOW7s)。

## 解释

说解释，其实还是需要用到牛顿力学的知识和一些数学工具。研究力学问题，第一步是描述物体的运动，即运动学。一个刚体在某一瞬间的运动可以用两个三维矢量来刻画。

1. 质心 $$\mathbf{x}_\mathrm{C}$$ 的速度 $$\mathbf{v}_\mathrm{C}=(v_x, v_y, v_z)$$。在材料密度均匀的情况下，一个刚体的质心、即质量中心，等于几何中心。
2. 围绕着质心的角速度 $$\Omega=(\omega_1, \omega_2, \omega_3)$$，方向指向此刻的旋转方向，大小 magnitude 为此刻旋转的速度，单位是 rad / s。

刚体上任意一点 $$\mathbf{x}$$ 的速度 $$\mathbf{v}$$ 可以由 $$\mathbf{v}_\mathrm{C}$$ 和 $$\Omega$$ 如下公式计算而得

$$
\mathbf{v}=\mathbf{v}_\mathrm{C} + \Omega\cross(\mathbf{x}-\mathbf{x}_\mathrm{C}).
$$

在没有外力的情况下，牛顿力学应用到刚体上有如下两个结论

1. 刚体线动量守恒

$$
m\mathbf{a}=m\ddot{\mathbf{x}}_\mathrm{C}=\mathbf{0}.
$$

2. 刚体角动量守恒

$$
\mathbf{I}\dot{\Omega}+\Omega\cross(\mathbf{I}\Omega)=\mathbf{0}.
$$

其中 $$\mathbf{I}$$ 为表述在随着刚体一起旋转的坐标系中的惯性张量。通常这个与刚体一起旋转的坐标系就取为刚体的旋转主轴坐标系，可得到 $\mathbf{I}=\mathrm{diag}(I_1, I_2, I_3)$。

<img src="/assets/images/2021/07/omega_1.svg" width="500px" />

ddd

<img src="/assets/images/2021/07/broken-phone-screen.png" width="600px" />

[^1]: 如果你把手机摔坏的话，也别忘了拍张类似上面的照片，用来研究裂纹的动态传播。
