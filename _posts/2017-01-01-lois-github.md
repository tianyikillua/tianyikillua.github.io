---
title: Nul n'est censé ignorer la loi
tags:
  - Git
  - 法律
  - 法国
header:
  image: /assets/images/2017/01/RepubliqueNum.jpg
  caption: © [gouvernement.fr](http://www.gouvernement.fr/)
---

这句话实际想表达的，不是说每个人都必须知道所有的法律，而是说不能以不知道法律而逃离法律的制裁。如果真的无知者无罪[^1]的话，那么每个人都可以用不知道某条法律为借口进行犯罪，法治就不可能存在。站在社会角度，无知者仍然有罪。

但站在个人角度，这句话严重威胁了公民的司法安全。想象一个不对公民公开法律的“法制”社会，那么这个社会完全是一个黑箱的存在，不仅打击了那些想遵守法律的公民，惩罚对于那些不小心触犯法律的公民也是不合理的。

在实际生活中，虽然不存在「不对公民公开法律」的情况，但是由于司法体系不完善或者技术问题，个人可能无法容易地获得自己想得到的法律信息。对于这个问题，法国的法国宪法委员会 Conseil Constitutionnel 在 1999 年做出决定[^2]，所有法律都必须在「可获得性 accessibilité 」和「清晰性 intelligibilité 」上达到一定条件。所以一开始这句话可以改成

> 无知者仍然有罪，除非法律本身难以获得或者撰写过于晦涩。

前段日子出于利益相关，稍微仔细地研究了法国的[外国人法典](https://www.legifrance.gouv.fr/affichCode.do?cidTexte=LEGITEXT000006070158)。通过[个人经历](/2016/11/23/for-laffi)，让我知道这个政府的确是法治的[^3]，更激发我对法律公开 Open Law、政府公开 Open Gouvernment、信息公开 Open Data 等产生兴趣。通过现在的信息技术，公民可以更容易地合作实现社会体系的完善，一个例子就是 2015 年法国的[数字共和国法案 Loi pour une république numérique](https://www.republique-numerique.fr)：公民可以通过互联网来参与法律的撰写。

在法律公开方面，法国主要是靠 [Legifrance](https://www.legifrance.gouv.fr) 这个网站，比如[最新的外国人法典](https://www.legifrance.gouv.fr/affichCode.do?cidTexte=LEGITEXT000006070158)和 2016 年通过的[外国人法](https://www.legifrance.gouv.fr/affichTexte.do?cidTexte=JORFTEXT000032164264&categorieLien=id)。你会发现我们实际想了解外国人权利的时候，应该去查询现在最新的**法典**，即包含了所有关于外国人的法律条款。而以前或这次新通过的外国人**法**，只是撰写了如何修改这部**法典**，描述了这次我们进行引入的改动。

熟悉版本控制（比如 `git` 或者 `hg`）的码农们可以发现法律和编程的相似之处：

- 都是在编写一个文本文件，比如一个法典
- 每次做出的改动 `commit` 可以对应每次议会对法典的修改
- 通过 `git checkout` 可以查看这次改动之后法典的样子

所以很多技术宅们就想到把法律用版本控制的方式进行管理，比如这里是法国的[民法](https://github.com/steeve/france.code-civil)。我最近更新了 Github 上的一个开源程序 [Archeo-Lex](https://github.com/Legilibre/Archeo-Lex)，并将其运用到了外国人法典上，获得了这个用 Markdown 撰写和 Git 管理的 [Repository](https://github.com/tianyikillua/ceseda)。法律条文就储存在 `Code_de_l’entree_et_du_sejour_des_etrangers_et_du_droit_d’asile.md` 文件中，而每次 `commit` 就对应了每次 Legifrance 上面的法律更新 Consolidation。

做了那么多事情，如果没有好处技术宅也不会去做的。如果你看 2016 年 3 月通过的[外国人法](https://www.legifrance.gouv.fr/affichTexte.do?cidTexte=JORFTEXT000032164264&categorieLien=id)，它对应了一个 `commit`，描述了对[法国人法典](https://www.legifrance.gouv.fr/affichCode.do?cidTexte=LEGITEXT000006070158)的修改。问题在于这个 `commit` 的表示形式对于人类是很不友好的，全文就傻傻地说法典的第几条第几句话中哪个字变成了哪个字，比如下面针对多年居留卡的一条法律条款：

> Le second alinéa de l'article L. 313-1 du même code est remplacé par deux alinéas ainsi rédigés : 
>
> « La durée de validité de la carte de séjour pluriannuelle ne peut être supérieure à quatre ans. 
>
> « A l'expiration de la durée de validité de sa carte, l'étranger doit quitter la France, à moins qu'il n'en obtienne le renouvellement ou qu'il ne lui soit délivré un autre document de séjour. »

通过引入版本控制，我们可以通过 `diff` 工具来描述每一次的改动 `commit`，上面的法律条款就可以更清晰地表示为（也可以看[这里](https://github.com/tianyikillua/ceseda/commit/7161015afe9fb31c87a77ad5ccb0a6752b00a9a4#diff-abb0b01853af70e296a9d8fa121176fbR905)）

[![]({{ site.url }}/assets/images/2017/01/Titre-pluriannuel.png)]({{ site.url }}/assets/images/2017/01/Titre-pluriannuel.png)

通过版本控制，每次对法律的改动可以用更直白的表现形式展现，使得我们可以更方便地了解一个法典在时间上的演化。

比如 2013 年 7 月 24 日的[改动](https://github.com/tianyikillua/ceseda/commit/0d98d2abafb6e4f4338e29bcf38d5d5b1ba5141e#diff-abb0b01853af70e296a9d8fa121176fbR687)就修改了外国学生在法求职的权利：之前只给一张 6 个月的 APS，之后给张 1 年的，而且不需要证明这份工作是为了今后回自己国家考虑，使得外国学生可以自行根据自己的计划在法国过人生。

[![]({{ site.url }}/assets/images/2017/01/APS.png)]({{ site.url }}/assets/images/2017/01/APS.png)

另外个例子，2014 年 8 月 22 日[修改](https://github.com/tianyikillua/ceseda/commit/125896de6f90ca4685bfaea2702e6c6e5678cee2#diff-abb0b01853af70e296a9d8fa121176fbR5553)了科技签，允许“科学家”在合同结束后可以去失业局注册失业领失业金，同时其居留证也必须自动更新至不能领失业金为止（2 年）。如果没这次修改，那我现在也不能写这篇文章了。

[![]({{ site.url }}/assets/images/2017/01/Scientifique.png)]({{ site.url }}/assets/images/2017/01/Scientifique.png)

这次 2016 年 10 月底正式实施的新外国人法的 `commit` 用 `diff` 的形式可以在[这里](https://github.com/tianyikillua/ceseda/commit/7161015afe9fb31c87a77ad5ccb0a6752b00a9a4)看到。相比[官方](https://www.legifrance.gouv.fr/affichTexte.do?cidTexte=JORFTEXT000032164264&categorieLien=id)给出的网站，这里更直观地显示出了改动。在我学习的过程中，发现了一个有意思的地方：

- 对于普通工签 salarié，如果失业的话，先自动给续 1 年，然后再根据领失业金的情况进行更新，也就是说再续 1 年：[点击这里](https://github.com/tianyikillua/ceseda/commit/7161015afe9fb31c87a77ad5ccb0a6752b00a9a4#diff-abb0b01853af70e296a9d8fa121176fbR1031)
- 对于这次新出来的 passeport-talent，如果失业的话，直接给续 2 年...哈哈：[点击这里看](https://github.com/tianyikillua/ceseda/commit/7161015afe9fb31c87a77ad5ccb0a6752b00a9a4#diff-abb0b01853af70e296a9d8fa121176fbR1216)

我觉得之后这一区别应该之后会被修改，salarié 也应该直接给续 2 年。我希望之后在做博士的科技签也可以和学生一样可以领个允许工作的 APS，这样我现在就不能傻等 4 个月了...不知道啥时候这个权利能被争取到。

[^1]: 如果不从字面来看，对「无知」的解释不是「不知道法律」，而是类似于「客观上不能对自己行为负责」，那么可以说「无知者无罪」，见[这个知乎问答](https://www.zhihu.com/question/38176398)。
[^2]: 见[这篇文章](http://www.conseil-constitutionnel.fr/conseil-constitutionnel/root/bank_mm/pdf/Conseil/secjur.pdf)。
[^3]: 也就是说哪一天至少行政部门可以被人工智能、机器人代替...