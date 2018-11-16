+++
title = "hugoの編集の仕方"
date = 2018-11-15T11:01:03+09:00
draft = false
tags = ["hugo"]
categories = ["hugo"]
+++
<!-- <pre></pre> -->
やっとこさhugoで**アウトプットブログ**が出来たのであれやこれやとhugoについてまとめてみる！初めての**Markdown記法**だからかなり見ずらいかもしれないけどすいません。**Markdown記法**も勉強しないと！

まず、自分はhugoディレクトリがあるからそこで<pre>hugo new site muublog</pre>それから<pre>cd muublog</pre>宣言する！<pre>git init</pre>テーマを追加する<pre>git clone https://github.com/avianto/hugo-kiera.git kiera</pre>追加をしたらthemesディレクトリに移動する<pre>cd themes</pre>今はthemesディレクトリが空だから<pre>git submodule add https://github.com/avianto/hugo-kiera.git kiera</pre>そして<pre>cd ..</pre>atomで開く<pre>atom .</pre>themesのconfig.tomlをコピーして、muublogのconfig.tomlに貼り付ける！<br>それから新しい投稿を追加<pre>hugo new posts/first-post.md</pre>これで<pre>hugo server -D</pre>出てきたlocalhostのURLをブラウザに貼り付けたら表示される。<br>次に新しくリポジトリを作ってpushする。<pre>git add .<br>git commit -m "first commit"<br>git remote add origin git@github.com:yourname/リポジトリ名.git<br>git push -u origin master</pre>次は本番環境で表示できる様にしてみる！<br>config.tomlを少しいじる<pre>baseurl = "https://yourname.github.io/リポジトリ名"<br>publishDir = "docs"を追加</pre>hugoコマンドでhtmlなどのファイルを作成<pre>hugo -t theme名<br>git add .<br>git commit -m "コミット名"<br>git checkout master<br>git merge ブランチ名<br>git push origin master</pre>次にリポジトリの設定を変更する<br>![サンプル](source.png)
