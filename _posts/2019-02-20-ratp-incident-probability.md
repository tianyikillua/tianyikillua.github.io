---
title: 为什么巴黎地铁又出问题了
excerpt: "为什么地铁 1 号线又出问题了？这篇博文尝试用统计的观点来分析下巴黎地铁系统每天都会发生的这些运营事故。"
tags:
  - RATP
  - 巴黎
  - 地铁
  - 统计
  - Python
header:
  image: /assets/images/2019/02/ratp.jpg
  caption: © [http://transportparis.canalblog.com](http://transportparis.canalblog.com)
---

**English version** Complete analysis report in English and source code can be directly found on [Github](https://github.com/tianyikillua/ratp-metro-incident).
{: .notice--info}

**Version française** Une version française de cet article est disponible sur [LinkedIn](https://www.linkedin.com/pulse/pourquoi-mon-m%C3%A9tro-est-toujours-perturb%C3%A9-quelques-r%C3%A9ponses-tianyi-li).
{: .notice--info}

为什么地铁 1 号线又出问题了？这篇博文尝试用统计的观点来分析下巴黎地铁系统每天都会发生的这些运营事故。

通过分析巴黎地铁运营公司 RATP 的官方推特（比如 1 号线账户是 [@Ligne1_RATP](https://twitter.com/Ligne1_RATP)），我建立了一个统计模型尝试回答如下问题

1. 在某一条地铁线上遇到运营故障的概率是多少？
2. 巴黎地铁的哪一条线最容易让你发火（你大概已经有答案了）？
3. 这些故障的主要原因是什么？
4. 如果我 8 月份继续上班而不度假，能找到一个让自己开心的理由吗？

<img src="/assets/images/2019/02/twitter_orig.png" width="600px" />

首先要强调一点（特别是对巴黎地铁系统不熟悉的读者），这里所说的「运营事故」指的是部分（比如某两站之间）或者完全（很少）中断，或者由于各种原因（比如中断后重启、地铁信号系统出故障等等）列车运行速度变慢。

## 我周三必须 17 点前离开公司（或者 21 点后）

下图是地铁 2 号线（我每天坐的线）在一个特定的星期和以每小时为单位的时间段遇到运营事故的概率。可以看到最大值 9% 位于周三 18 点到 19 点，而且从 17 点到 21 点出故障的机率一直很高。

<img src="/assets/images/2019/02/hour-weekday.png" width="600px" />

当然，避开早晚高峰段以及在周末（尤其是周日直到傍晚） 2 号线还是挺平静的。

## 乘客是主要事故原因（至少 2 号线上）

几乎一半（48%）的运营事故是由乘客造成的：轨道上出现乘客[^1]、恶意行为[^2]、警报按钮启动[^3]、人流量大（嗯……）。除此之外，2 号线上 9% 的事故是因为发现可疑包裹，当然大多数情况下只是乘客忘记了。

<img src="/assets/images/2019/02/causes.png" width="550px" />

相比较，下图是 14 号线的事故主要原因。14 号线从开始运营起就是条全自动的地铁线路。它出故障机率低（马上会看到），而且受乘客行为影响也不大（当然也因为 14 号线很短，单程只需要 15 分钟）。它的主要事故原因是技术起因，比如列车出故障或者铁轨断裂……

<img src="/assets/images/2019/02/cause_14.png" width="550px" />

## 13 号线被 4 号线打败了

住在巴黎的人都知道 13 号线是条最恐怖的线（不管是不是传说还是亲生经历）。但在 2018 年它被它的兄弟 4 号线打败了：平均 4 号线出故障的概率是 4%。

<img src="/assets/images/2019/02/palmares.png" width="600px" />

可以看到相比我的 2 号线还是挺好的，它甚至排在 1 号线（是条从人工变成全自动的地铁）之后。

出故障最少的的确是 14 号线，不过前面也说过除了因为它全自动，它本身也很短。

## 巴黎（地铁） 8 月份才去度假

下图比较了每条线（颜色参考了 RATP 官方地铁，见上图） 2018 年平均出故障机率和 8 月份的机率。可以发现在 8 月份出故障机率可以下降 2%：比如 4 号线的故障机率从 4% 下降到 2%。本来出故障最少的 10 和 14 号线稍微上升了一点点……

<img src="/assets/images/2019/02/august.png" width="600px" />

如果我们分析 5 月份和 7 月份，会发现 5 月份的下降趋势没有这么明显（尽管 2018 年 5 月份放假很多），而 7 月份完全没有区别，说明巴黎人 / 地铁还在努力上班。

## 统计分析方法和源代码

完整分析报告（英语）和源代码可以在 [Github](https://github.com/tianyikillua/ratp-metro-incident) 上找到。

数据分析和图片运用了 Python 库 pandas 和 matplotlib，欢迎进行改动。

[^1]: 比如列车中断了很久，乘客受不了就打开车厢直接在轨道上走了。
[^2]: 比如在轨道上放块石头之类的……？
[^3]: 一般情况下是因为乘客突然身体不舒服晕过去了，这种情况下列车要停下来，等救护人员赶到车站照顾伤者，之后才可以重新启动。