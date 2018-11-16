+++
title = "hugoの編集"
date = 2018-11-16T16:25:17+09:00
draft = true
tags = ["hugo"]
categories = ["hugo"]
+++

hugoのインストールから本番デプロイまでをまとめられたから次はhugoの**編集の仕方**を少しまとめてみようと思う！
***
**新しく記事を作成**
```
hugo new posts/secound.md
(secoudのとこはなんでも良い)
```
postsディレクトリにsecound.mdが追加される、
これはその中身
```
title = "secound"
date = 2018-11-16T16:25:17+09:00
draft = true(falseにすると本番にデプロイ出来る)
tags = []
categories = []
```
```
tags = []
categories = []
```
これは
```
tags = ["hugo"]
categories = ["hugo"]
```
の様にしてから
```
hugo -t theme名
```
にすると、<br>categoriesディレクトリとtagsディレクトリに勝手に生成してくれる。
***
topページの編集はconfig.toml

profileページの編集はabout.md

blog & autputページの編集は_index.md
