---
title: Legendre 变换
tags:
  - 数学
---

...今天泡了大半天 Pompidou 图书馆加上网上一个超好的文章 [Legendre-Fenchel transforms in a nutshell](http://www.maths.qmul.ac.uk/~ht/archive/lfth2.pdf) 终于搞清楚点了这个超级好玩的变换...我说的好玩是指乍眼难以看清它在干什么...

由于已经晚上了...现在不想写得太详细[^1]，所以就说说定义和一些结论。设 $$f:\mathbb{R}^n\to\mathbb{R}\cup\{+\infty\}$$，其 LF 变换定义为 

$$
f^*(k)=\sup_{x\in\mathbb{R}^n}\left(\langle k,x\rangle-f(x)\right)
$$

下面是关于 LF 变换的几个结论，以后再补充。

- 点变成斜率；把斜率变成点。
- 不可导点变成一段上的线性函数。比如把 $$x\mapsto\lvert x\rvert$$ 变成 $$[-1,1]$$ 的指示函数（在集合内为零，在集合外为正无穷）
- 若 $$f$$ 在 $$x$$ 处可导且导数为 $$k$$，那么 $$f^*$$ 在 $$k$$ 处可导而且导数为 $$x$$

$$
k\in\partial f(x)\iff x\in\partial f^*(k)
$$

[^1]: 其实也写不了很详细