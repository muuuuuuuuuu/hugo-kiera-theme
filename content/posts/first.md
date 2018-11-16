+++
title = "hugoのテーマをインストールから本番デプロイまで"
date = 2018-11-15T11:01:03+09:00
draft = false
tags = ["hugo"]
categories = ["hugo"]
+++
<!-- <pre></pre> -->
やっとこさhugoで**アウトプットブログ**が出来たのであれやこれやとhugoについてまとめてみる！初めての**Markdown記法**だからかなり見ずらいかもしれないけどすいません。**Markdown記法**も勉強しないと！

まず、自分はhugoディレクトリがあるからそこで
```
hugo new site muublog
```
それから
```
cd muublog
```
宣言する！
```
git init
```
テーマを追加する
```
git clone https://github.com/avianto/hugo-kiera.git kiera
```
追加をしたらthemesディレクトリに移動する
```
cd themes
```
今はthemesディレクトリが空だから
```
git submodule add https://github.com/avianto/hugo-kiera.git kiera
```
そして
```
cd ..
```
atomで開く
```
atom .
```
themesのconfig.tomlをコピーして、muublogのconfig.tomlに貼り付ける！<br>それから新しい投稿を追加
```
hugo new posts/first-post.md
```
これで
```
hugo server -D
```
出てきたlocalhostのURLをブラウザに貼り付けたら表示される。<br>次に新しくリポジトリを作ってpushする。
```
git add .
git commit -m "first commit"
git remote add origin git@github.com:yourname/リポジトリ名.git
git push -u origin master
```
次は本番環境で表示できる様にしてみる！<br>config.tomlを少しいじる

```config.toml
baseurl = "https://yourname.github.io/リポジトリ名"
publishDir = "docs"
```

を追加</pre>hugoコマンドでhtmlなどのファイルを作成
```
hugo -t theme名
```
```
git add .
git commit -m "コミット名"
git checkout master
git merge ブランチ名
git push origin master
```
次にリポジトリの設定を変更する<br>SettingからGithub pagesのSourceを<br>master branch/docs folderにしてsaveするとURLが吐き出される。
```
https://muuuuuuuuuu.github.io/myproject3/
```
こんな感じで本番にデプロイ出来ました！
