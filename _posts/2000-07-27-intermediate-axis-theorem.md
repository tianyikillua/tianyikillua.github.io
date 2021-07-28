---
title: 一个力学小知识
tags:
  - 力学
words_per_minute: 10
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

如果实在不想弄坏自己的手机或者书的话，也可以看看下面这个视频。

{% include video id="l51LcwHOW7s" provider="youtube" %}

## 解释

<img src="/assets/images/2021/07/omega_1.svg" width="500px" />

ddd

[^1]: 如果你把手机摔坏的话，也别忘了拍张类似下面的照片，用来研究裂纹的动态传播。

<img src="/assets/images/2021/07/broken-phone-screen.png" width="600px" />
