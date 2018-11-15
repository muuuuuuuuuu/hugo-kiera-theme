+++
title = "hugoの編集の仕方"
date = 2018-11-15T11:01:03+09:00
draft = false
tags = ["hugo"]
categories = ["hugo"]
+++
<!-- <pre></pre> -->
やっとこさhugoで**アウトプットブログ**が出来たのであれやこれやとhugoについてまとめてみる！初めての**Markdown記法**だからかなり見ずらいかもしれないけどすいません。**Markdown記法**も勉強しないと！

まず、自分はhugoディレクトリがあるからそこで<pre>hugo new site muublog</pre>それから<pre>cd muublog</pre>宣言する！<pre>git init</pre>テーマを追加する<pre>git clone https://github.com/avianto/hugo-kiera.git kiera</pre>追加をしたらthemesディレクトリに移動する<pre>cd themes</pre>今はthemesディレクトリが空だから<pre>git submodule add https://github.com/avianto/hugo-kiera.git kiera</pre>そして<pre>cd ..</pre>atomで開く<pre>atom .</pre>themesのconfig.tomlをコピーして、muublogのconfig.tomlに貼り付ける！
