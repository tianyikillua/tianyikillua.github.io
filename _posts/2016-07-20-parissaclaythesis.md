---
title: Template LaTeX pour les thèses de l'Université Paris-Saclay
tags:
  - 博士
  - LaTeX
last_modified_at: 2017-03-12
---

正以为自己开始走出抑郁症的时候，今天 Saint-Goblin 却告诉我没被录用。昨天晚上又在重温“[冷暖人间](https://movie.douban.com/subject/1997612/)”，突然听到一句话，觉得挺好的：

> 意外总在某处等你，等着你把它解决。

---

博士论文差不多一个月前写好了，因为 10 月份答辩，所以理论上应该是正好按照规定（3 个月）...但发现有些比我早面试的都还没写好...原来自己又提前做完了工作。

定答辩时间到没有发生什么意外的事情：就是不是很简单，有些人行有些人不行，不过只发过一次 doodle，所以也没很麻烦。地点到是有点悬，EDF 不行，X 也不行，还好 ENSTA 还有地方。

我应该算是第一批 Paris-Saclay 大学的博士生，这个东西官方都承认了，就是为了对付上海交通大学大学排名。谁叫法国大学、研究机构都太小了，从数量上比不过其他学校。我看过其他一个排名，说是全球小型大学排名中，法国还是挺牛逼的...可惜为了吸引各地有钱的留学生么，不得不增加法国的学术吸引力...

Paris-Saclay 博士论文的官方样板在[这里](https://www.universite-paris-saclay.fr/fr/doctorat/documents-de-reference/soutenance-de-la-these)，可以不仅仅只是 Word 版本的，而且各种图片文件都是位图，不是可以随意缩放的矢量图，这让我这个完美主义者很尴尬...

当时写的时候[发现](https://www.institutoptique.fr/Institut/Mediatheque/Depot-legal-des-theses-de-l-Institut-d-Optique-Graduate-School/Rediger-votre-these)了一个 LaTeX 的封面和最后一页的模版，可惜对有些字体排版不是很满意，而且还是没有矢量图。这里在下面给出我用的模版和矢量图，我是用 `potrace` 和 `Inkscape` 把官方的位图转成了矢量图。前者只支持单色，但感觉质量比较好；后者貌似是前面的一个扩展，支持多颜色。

---

封面 / Page de garde

下面是所做出一些字体微改后的论文封面，如果喜欢的话去我的 Bitbucket 下载，在：[https://bitbucket.org/litianyi/thesis-manuscript](https://bitbucket.org/litianyi/thesis-manuscript) / Voici un template LaTeX pour la page de garde que vous retrouverez sur mon repository Bitbucket.

之后找 `thesis-manuscript/auxfiles/titlepage.tex` 就可以了。

矢量化（通过 `potrace` 软件）的 Paris-Saclay 的 logo 和 Ecole Polytechnique 的 logo 也可以在我的 Bitbucket 的 [Downloads](https://bitbucket.org/litianyi/thesis-manuscript/downloads/) 页面找到 / Les logos vectorisés de Paris-Saclay et de l'École Polytechnique se trouvent aussi dans mon repository Bitbucket ([Downloads](https://bitbucket.org/litianyi/thesis-manuscript/downloads/)).

[![]({{ site.url }}/assets/images/2016/07/Thesis-cover.png)]({{ site.url }}/assets/images/2016/07/Thesis-cover.png)

---

最后一页 / 4ème couverture

LaTeX 源文件在这里：`thesis-manuscript/chapters/backcover.tex` / Source LaTeX de la 4ème couverture.

由于我是 SMEMAG 的博士生，所以我就把它的 logo 给矢量化了（用 `Inkscape` 我记得，因为是多色）。同样，图片都在 Bitbucket 的 [Downloads](https://bitbucket.org/litianyi/thesis-manuscript/downloads/) 页面 / Les figures vectoisées utilisées dans la 4ème couverture sont aussi téléchargeable dans le package complet `Figs.7z` sur le site Bitbucket ([Downloads](https://bitbucket.org/litianyi/thesis-manuscript/downloads/)).

---

主文件 / Fichier principal

LaTeX 源文件在这里：`thesis-manuscript/main.tex` / Le fichier principal.

代码 `\usepackage[a-1b]{pdfx}` 是为了生成符合 PDF/A 标准的文件，为了之后博士论文的归档，这个是[规定](https://facile.cines.fr/) / La commande `\usepackage[a-1b]{pdfx}` permet de générer un fichier PDF compatible avec la norme PDF/A pour des fins d'archivage, cf. [ici](https://facile.cines.fr/).

```latex
\begin{filecontents*}{\jobname.xmpdata}
\Title{Gradient-Damage Modeling of Dynamic Brittle Fracture: Variational Principles and Numerical Simulations}
\Author{Tianyi Li}
\Subject{PhD thesis}
\Keywords{dynamic brittle fracture\sep gradient damage models\sep phase-field\sep variational methods\sep numerical implementation}
\end{filecontents*}
```

加载文件类型和引言 / Définir la classe et charger le fichier préambule

```latex
\documentclass[a4paper,11pt,twoside]{book}
\input{auxfiles/preambule}
```

BibLaTeX

```latex
\addbibresource{../thesis/Papers/biblio.bib}
```

各个章节 / Les chapitres

```latex
\begin{document}
\dominitoc
\frontmatter
\pagestyle{plain}

\input{auxfiles/titlepage}
\include{chapters/frontmatter}

\setcounter{tocdepth}{1}
\tableofcontents

\mainmatter
\pagestyle{fancy}
\include{chapters/introduction}
\include{chapters/formulation}
\include{chapters/numerics}
\include{chapters/simulations}
\include{chapters/conclusion}
\include{chapters/appendices}

\backmatter
\printbibliography[notcategory=fullcited]
```

保证最后一页是偶数页 / Assurer que la 4ème couverture soit une page paire.

```latex
\cleartoleftpage
\let\cleardoublepage\clearpage
\input{chapters/backcover}
\end{document}
```

> 2017年3月12日更新了链接。
