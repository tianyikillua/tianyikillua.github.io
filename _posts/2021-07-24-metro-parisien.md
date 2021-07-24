---
title: 巴黎地铁两个冷知识
tags:
  - 巴黎
  - 地铁
  - RATP
header:
  image: /assets/images/2021/07/nichijou.jpg
words_per_minute: 10
---
这周请了年假，感觉非常充实、轻松和舒服。意识到一直以来自己超我的强大，对自己有很多要求，压抑了自己的本我，于是开始要学会怎么放纵自己。不过雅雅说，也不能就因此就否定自己的超我；好好利用它就好了。

心理咨询师[^1]叫我想想自己写博客的原因，嗯……我想想，尽管大致已经有了几个答案。

## 吉祥物

周一去了次宜家，在地铁站 Madeleine 看到了这个可爱的贴示（应该已经很久了，因为记得以前也看到过）。

<img src="/assets/images/2021/07/serge.jpg" width="600px" />

大家知道为什么是兔子吗？没错哟，这只兔子就是巴黎地铁的“吉祥物”[^2]，名字叫 **Serge**。可以在[这个 RATP 的页面](https://www.ratp.fr/serge-le-lapin)上看到，它有过很多个版本，变得越来越潮和会打扮了😃。从 2014 年开始，开始穿牛仔裤和运动鞋了。

[<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f3/Evolution_Lapin_Serge.jpg/1280px-Evolution_Lapin_Serge.jpg" width="800px" />](https://fr.wikipedia.org/wiki/Lapin_du_m%C3%A9tro_parisien#/media/Fichier:Evolution_Lapin_Serge.jpg)

## 体验巴黎所有地铁的最省路线

如果你是巴黎地铁的爱好者，想体验下巴黎每条地铁（一共有 14 + 2 条线，因为有 3bis 和 7bis）的感觉，但又不想花很多时间，那么下面就会告诉你答案。对数学感兴趣的读者可以参考这篇 [arXiv 预印本](https://arxiv.org/abs/1709.05948)和这篇 [interstices.info](https://interstices.info/quel-trajet-optimal-pour-passer-au-moins-une-fois-par-toutes-les-lignes-de-metro/) 的博客。

通过[图论](https://en.wikipedia.org/wiki/Graph_theory)的一些概念，这个问题可以转变成一个数学上的最优化问题。对于「最省路线」，一般人类关心的是”最短时间”。由于具体乘坐时间取决于[巴黎地铁是不是出了问题](/2019/02/20/2019-02-20-ratp-incident-probability)、司机开车的熟练程度、在转线时你的走路速度（这取决于你本身的走路速度和人群的多少）等等，所以我们也使用[圆形奶牛](https://en.wikipedia.org/wiki/Spherical_cow)来简化问题：这里「最省」指的是通过最少的地铁站台。

一个数学问题通常可以有很多种具现化的描述方式。学生时代在做[桁架拓扑优化问题](2012/05/20/optimisationtopo)的时候明白，一个非线性优化问题事实上可以通过重新 formulation 的方式，转变为一个[线性规划问题](https://en.wikipedia.org/wiki/Linear_programming)。对于这个最省路线问题同样，可以证明[^3]这个问题可以用一个（整数）线性规划问题来描述。

省去详细的数学推理，下面给出答案。体验巴黎一共 16 条线最少需要 26 步，即需要经过 27 站。需要注意是这个不是一个唯一解，因为可以从 6 号线 Cambronne 开始，也可以从 10 号线的 	Avenue Emile Zola 开始。但是这个路线不能反过来坐，因为 7bis 上的有些路线是[单向](/2014/02/04/parismetro)的。

<img src="https://interstices.info/wp-content/uploads/2020/10/metro_figure1-1024x559.jpg"/>

我稍微对这个建模不是很满意的就是，它是一个全局最优解，而没有考虑你出发的站台。假设你从 Nation 出发，那么最佳路线肯定不是上面一条，需要通过的站台肯定大于 27 站。不过数学上要解决这个“局部优化问题”很简单，只需要强行将那个站的 variable 设为必须出现。哪位感兴趣的同学可以编个程解决这个问题哈。

[^1]: 对，结果我又开始见她了-_-
[^2]: 类似上海地铁的「[畅畅](https://baike.baidu.com/item/%E7%95%85%E7%95%85/7773893)」
[^3]: 而且是“建设性的证明”
