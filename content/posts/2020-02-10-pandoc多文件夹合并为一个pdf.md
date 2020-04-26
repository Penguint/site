---
layout: post
title: 证明：LCS(A, sort(A)) = LNDS(A)
date: 2020-02-10 23:34
category: 
author: Penguint
tags: []
summary: 
excerpt_separator: <!-- more -->
---
<!-- more -->

> 一定要纪念一下这个由于不会写 PowerShell 而疯狂调试了 5 个小时命令的晚上。我敢说没有人会像我一样蠢到肉眼逐字符比较两行长得一模一样的命令，然后发现 Pandoc 报错的原因竟是宋体的英文名大小写打错...

麻烦的开始：为了可以方便地更新板子，把板子拆成单文件，并分文件夹整理。

麻烦的进击：为了在更新板子之后，可以将所有文件一键自动化合并成一个 PDF，不得不使用 Pandoc。同时也借此机会可以折腾一下 $\LaTeX$，让板子变得酷炫一些。

麻烦的解决：自动化生成板子的命令：
```shell
pandoc $(ls -r -I *.md -n -E README.md,ICPC模板.md,cover.md)  -s -o ICPC.pdf --pdf-engine=xelatex -V CJKmainfont='SimSun' -N --toc
```

不会用 PowerShell。不会用 VSCode。于是效率非常低的折腾了一晚上。

不过现在的板子可以一键生成，可以用 $\LaTeX$ 模板，可以自动标号...是舒服了不少。