---
title: Changement de statut vers "Passeport-talent salarié"
tags:
  - Préfecture
  - Carte de séjour
  - 法国
  - Python
---

在 2016 年 11 月底的[这篇博文](/2016/11/23/for-laffi)和[这篇](/2017/01/01/lois-github)之后，来分享下自己申请 *Passeport-talent salarié* 长居卡的经历。尽管之前已经把具体地理情况说过了，如今既不想去删掉这些信息，也不想再在这里重复说明，这篇文章不是去指责谁什么，只是分享下经历和进行理性的分析。仅以此博文正式马克下这段体验的结束和新工作的开始。

### 黑箱的输入和输出

如果把这次换长居卡的经历看作黑箱，那么可以稍微总结下输入和输出。

- 2016 年 9 月 30 日我的 Carte de séjour temporaire *Scientifique-Chercheur*[^1] 过期；
- 2017 年 4 月 21 日拿到新的有效期到 2021 年的 Carte de séjour pluriannuelle *Passeport-talent salarié*；
- 一共换了 4 张 Récépissés；
- 如果这个黑箱有名字，那么它的名字是「运气」。

### 时间轴

借助 Google Timeline 和一点点 [Python](https://www.dropbox.com/s/n1kgnm701yrdds5/pref94.py)，可以把这次为了换身份跑 préfecture 的时间轴表现在下图中。横轴记录了每次去 préfecture 的日期，柱形图和纵轴标出了每次所花费的时间区间，最上方标题处则计算了一共所消耗的小时数。正如上面所说，这篇文章不是想去重新“描述” préfecture 的接待条件，关于这点已经可以从法国内政部的[众多报告](http://www.immigration.interieur.gouv.fr/Info-ressources/Documentation/Rapports-publics)和 [circulaires](http://www.gisti.org/spip.php?rubrique110#139) 中可以知道，但至少应该知道这张图片本质上是用身体画的……

[![]({{ site.url }}/assets/images/2017/04/pref94.png)]({{ site.url }}/assets/images/2017/04/pref94.png)

- 2016 年 6 月 30 日：“物理”“生态”预约更新快过期的 *Chercheur* 长居，约到下面这个日子；
- 2016 年 9 月 2 日：递交更新 *Chercheur* 长居的材料。由于我没有新的 Convention d'accueil，所以是按照「拿失业金」作为理由更新的。正如[这篇博文](/2017/01/01/lois-github)里所说，这个理由的合法性是 2014 年之后才确立的。2 年后至少按照我的经历 préfecture 还是很好地贯彻了这条法律。由于根据这个理由更新长居卡需要 Pole emploi 的证明，而在 Pole emploi 注册需要有效的长居卡，在实践中咱们可爱的 préfecture 打破了这个死循环，一般会先给你一张 récépissé，你拿着这个临时的长居去注册失业，然后再回 préfecture 交注册证明，然后拿续好的长居。我这张 récépissé 是 16 年 12 月 29 日过期。从 [Circulaire du 3 janvier 2014 relative à l'amélioration de l’accueil des étrangers en préfecture et aux mesures de simplification et objectifs d'organisation](https://www.dropbox.com/s/r486d2gon35esrf/circ-2014-01-04.pdf) 之后，续长居的时候给你的 récépissé 的有效期从你现有长居卡的过期日开始算，而不是你申请续长居的日期（如果是这样，我这张 récépissé 的有效期就只到 12 月 1 日 ）；和 Guichet 说之后马上可能会需要换成工签，给了我张每天 10 点 convocation；
- 2016 年 11 月上旬：和新公司谈妥，开始准备工签的材料。开始了解外国人法，特别是新的 *Passeport-talent* 长居卡，可以从[这篇博文](/2016/11/23/for-laffi)中看到；
- 2016 年 11 月 25 日和 28 日：凭借之前给的 convocation 去递交工签材料。25 号说那天换身份的人太多，所以 28 号去才递交“成功”，看图可以发现那一整天都待在里面了。交材料的时候那个人不清楚 *Passeport-talent salarié* 的情况，收下所有材料之后说会“研究”我的材料。拿到一张新的到 2 月 27 日的 récépissé，标注是 *Exercice d'une activité salariée*。根据外国人法，第一次申请各种[^2] *Passeport-talent* 的 récépissé 在 préfecture 处理完你的档案之前不能工作（除非你有使馆给你的 Visa）。有意思的是之前如果你第一次申请 *Scientifique*，那你凭借这个 récépissé 可以工作；
- 2017 年 2 月 20 日和 28 日：2 月初回到法国后发现仍然没有消息（没有 préfecture 的信）。根据 préfecture 的要求寄了封信，说申请了 *Passeport-talent salarié* 仍然没有消息，附上了一些基本的材料，为了续 récépissé。20 日去排队，guichet 没什么有用的消息给我，除了透露了说它们还在等我的 Pole-emploi 证明。那个时候还以为它们把我续 *Scientifique* 长居和申请 *Passeport-talent salarié* 的材料给搞混了。2 月 27 日也就是 récépissé 过期的那天收到 préfecture 的信，附上了新的到 5 月 21 日的 récépissé。信上说它们还在等我的 Pole-emploi 注册证明或工作合同，于是真的感觉它们混淆了两个材料，于是第二天凭借这封信下午 2 点把合同给了 guichet，还加上了自己打印的一封解释信，说申请的是 *Passeport-talent salarié*。之后叫新公司的老板写信给 préfecture 询问情况，还跑了次维护外国人权益的社团（没啥结果不过，我觉得我这种情况它们根本不在乎，它们在乎的是帮那些黑工合法化等更“严重”的事情，所以我其实被夹在了中间）；
- 2017 年 3 月 28 日：由于还没有消息，于是再次一早上去排队询问情况。由于已经 4 个月过去了，所以事实上按照法律，我的档案其实已经被拒了（refus implicite），当然现实情况不是（但我可以以此写信去申诉）。去的时候就告诉自己没有结果不会离开，幸好这次遇到一个稍微负责的员工（当初 9 月 2 日续 *Scientifique* 长居的时候也是他），拿出新外国人法的 [circulaire](https://www.dropbox.com/s/4kavob43lp4ev8r/circ-2016-11-02.pdf)，然后解释了自己的情况，于是很罕见地去找了我的档案（之前的员工都只是在电脑上看看情况，没有具体去找我的档案），说没有我当初给它们的合同。于是我知道它们丢失了我 11 月 28 日给的关于公司的材料（放在一个信封里面）。看到我的博士文凭（哎）之后，他叫我过几天拿着合同去找他，也没有叫我重新交其他公司的材料。
- 2017 年 3 月 30 日：29 号重新去找了次新公司，拿到了之前已经交过的材料（合同啥的），然后 30 号再重新给了这个员工。我询问（要求？）是否可以开始工作，他迟疑了下，运气好的是他知道它们肯定出了问题，所以当场就快速 valider（打发？）了我的档案，然后给了我张新的到 6 月 29 日的 Récépissé。由于已经在它们的电脑中 validé，于是在我的 récépissé 上手写了 Il autorise son titulaire à travailler。我的长居卡也终于处于“正在制作”的状态。
- 2017 年 4 月 21 日：差不多三周后（我本来以为还要更快），终于收到短信（天哪，它们终于知道有短信[^3]这个东西了，用短信通知拿长居卡同样是这个 [circulaire](https://www.dropbox.com/s/r486d2gon35esrf/circ-2014-01-04.pdf) 之后开始推广的，比如之前 Antony 就已经体验过了，没想到到 2017 年现在它们才开始）说可以去取了。拿到了长居卡，本来以为标注会和签证一样会比较隐晦地说是根据外国人法 L. 313-20 - 1° 签发的长居卡，结果还是很直白地标注为 *Passeport talent : Salarié qualifié / Entreprise innovante - Exercice d'une activité salariée*，也就是翻译了 L. 313-20 - 1° 条款。有效期开始日期果然是 3 月 30 日，即我的档案被当场 validé 的那天。还是根据这个 [circulaire](https://www.dropbox.com/s/r486d2gon35esrf/circ-2014-01-04.pdf)，现在长居的有效期开始时间为档案 validé 的那天，而不是之前长居过期的第二天。

### 猜测

3 月 30 号隐约从这位员工的话中听到些有意思的东西，下面就做下根据我对它们工作方式所做的一些猜测。法国对于我们外国人的居留管理采用的是 [AGDREF](https://fr.wikipedia.org/wiki/Application_de_gestion_des_dossiers_des_ressortissants_%C3%A9trangers_en_France) 软件系统（当然有过很多次修改和更新，现在貌似应该是 AGDREF2）。每次你去更新长居的时候，为了给你一张 récépissé 窗口必须记录你申请的长居信息，其中就包括新长居的类型码 code Agdref。如下图和这个 [Fiche](https://www.dropbox.com/s/s7ngv167832kw4j/CSP2-1.pdf)，我所申请的 *Passeport-talent salarié* 所对应的编码就是 4801。每个编码对应一个外国人法具体条款所规定的长居卡类型、申请理由和对应的法定材料。我当天听到他在系统里面找这个 code，然后说到 48...于是我就知道他没搞错。他期间还说好像我 11 月 28 号第一次交材料的时候的那个人就搞错这个 code，可能是搞成了普通的 Salarié 签（对应的 code 是 1203，见这个 [fiche](https://www.dropbox.com/s/l9rf0mfq8yt9xq6/CST3.pdf)），这就是为什么那个时候我拿到了一张标注为 *Exercice d'une activité salariée* 的 récépissé，因为当 DIRECCTE 给了工作许可之后，第一次申请 salarié 的 récépissé 允许工作。

[![]({{ site.url }}/assets/images/2017/04/CSP2-1.png)]({{ site.url }}/assets/images/2017/04/CSP2-1.png)

关于为什么它们丢了我的材料，我想应该是这样的。如果真的如我上面所说，它们应该就是把和公司和工作相关的材料寄给了 DIRECCTE，这就是为什么 3 月 28 号他找不到工签的表格、合同和其他公司的材料的原因。不过如果是这样的话，为什么 DIRECCTE 没有给我任何消息……？

### 感想

正如一开始所说，最终拿到长居卡真的只是「运气」：能够碰到那个负责的员工。很遗憾的是在新外国人法实施的 4 个多月后，他们对 *Passeport-talent* 长居卡还不是特别了解，以至于我每次都需要拿出自己打印的 [circulaire](https://www.dropbox.com/s/4kavob43lp4ev8r/circ-2016-11-02.pdf) 来解释。我不知道这一切是不是因为我做得太多而引起的……也许我一开始就不应该申请 *Passeport-talent salarié* 长居，而是普通的工签。不过那样的话网上已经说 DIRECCTE 会把档案退回到 Préfecture 叫 Préfecture 直接解决（因为符合 *Passeport-talent* 的材料 Préfecture 可以直接给长居，不需要工作许可），这样也会耽误时间。反之，像我这样直接和 Préfecture 说申请 *Passeport-talent*，它们又不清楚具体条款，结果搞错也耽误了时间。幸好我打印和仔细学习了法律条款，否则我这个档案永远不会被解决。

这就是很讽刺的地方。本身 *Passeport-talent* 的创立就是希望能够缩短档案处理的时间，但由于很多很复杂的原因（培训？）导致花了更长的时间。Préfecture 至少还是希望法治的（否则会无视我打印的法律，通过这次经历，知道懂点法律还是挺有用的），问题是在实践上还有很多不够主动的地方。不过站在它们的角度来看，由于外国人法一直在修改，所以的确很复杂……

[^1]: 也就是新的 Carte de séjour *Passeport-talent chercheur*
[^2]: 很多人还不知道其实 *Passeport-talent* 其实是很多个长居类型（比如科研、艺术家等）合并起来的 Marketing 产物
[^3]: 我之所以这么推测是因为之前交材料的时候窗口都没询问我的手机号而是要信封，而 3 月 30 号那天那个员工问了我的手机号，说会收到短信通知