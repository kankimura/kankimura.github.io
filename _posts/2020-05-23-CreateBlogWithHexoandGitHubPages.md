---
layout: post
title: "HexoとGithub Pagesで簡単にブログを作る"
description: "A graphic designer is a professional within the graphic design and graphic arts industry."
date: 2020-05-23
feature_image: images/road.jpg
tags: [tips, work]
---

hexoとGithub Pageでブログを作成したので、作成方法を説明します。
無料で簡単に作ることが出来たので、個人ブログをもちたい場合はオススメです。

<!--more-->

# Jekyllとは？

Jekyll(ジキル)とは静的サイトジェネレーターの一つです。
静的サイトジェネレータとはマークダウン式の記事とテーマをもとに静的ファイル（html/css/javascript）を自動生成してくれるツールです。<br>
自動生成されたファイルをGitHubPages等のホスティングサイトにアップすることでブログを簡単に公開することが出来ます。<br>
マークダウン方式の書き方さえ分かればコードは書く必要がないので非常に楽です。<br>
JekyllはRubyという言語で作られています。
Jekyll以外にも主要なものでGatsby、Hugo、Hexoといったものがありますが、私が知る範囲ではJekyllとHexoはテーマをサイトからダウンロード出来てマークダウン記事と作成したするだけで良いので、簡単にやりたい場合はどちらかを選ぶと思います。
Hexoは中国が開発元で、ググって見ても中国語の情報が多かったのでJekyllにしました。

マークダウン式がわからない方は以下を参考にしてみて下さい。
[https://qiita.com/Blueman81/items/72ca43681d16d44e21ad](https://qiita.com/Blueman81/items/72ca43681d16d44e21ad){:target="_blank"}

# Github Pageとは？
GitHubPagesとはGitHubによる静的サイトのホスティングサービスです。
GitHubのアカウントがあれば無料で使用することが出来るので、気軽にブログを始める事ができます。
ちょっと前まではブログを作るとなるとWordpressとかを使う必要がありましたが、サーバーのレンタル料金がかかってしまうので、それが無料になるのは素晴らしい事です。


HexoとGithubPageの関係を絵で表すと以下のようになります。

![jekyll-github](2020-05-24/images/jekyll-github-pages.png)

全体的な流れは以下のようになります。
①マークダウン方式の記事を作成<br>
②記事とテーマをもとにhtml/css/javascriptを生成<br>
③生成されたファイルをGitHubPagesにアップ<br>
④ブラウザからアクセスし、GitHubPagesにアップされたファイルを画面に表示する。

では実際にブログを作成して公開するまでの手順を説明します。

1.必要なライブラリのダウンロード
・Jekyllのダウンロード
2.GitHubアカウントの登録
2.GitHubリポジトリの作成

### 環境構築
#### Rubyのインストール
バージョン管理のためにrbenv,ruby-builをインストール
```
$ brew install rbenv ruby-build
$ echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
$ source ~/.bash_profile
```
インストールするRubyのバージョンを指定してRubyをインストール
```
$ rbenv install -l      //これで表示される最新のバージョンを指定する
$ rbenv install 2.6.0
$ rbenv global 2.6.0    //デフォルトで使用するバージョンを指定
```
#### Jekyllのインストール
```
$ gem install jekyll bundler    //Gem管理ツールbundlerとJekyllのインストール
$ jekyll new blog               //Jekyll用のディレクトリを作成
$ cd blog
$ bundle exec jekyll serve      //Jekyllをローカルで起動
```
http://localhost:4000 へアクセスしローカル環境でサイトが表示されていることを確認します。
ローカルで確認する際はbundle exec jekyll serveというコマンドでJekyllを起動する必要があります。
起動中に記事を編集しても反映されるので編集しても再起動する必要はありません。
このままだとインターネットからアクセス出来ないので、GitHub Pagesに公開する必要があります。
その前にブログで使用するテーマをダウンロードしたいと思います。

### テーマのダウンロード
今のままだとデフォルトのテーマで味気がないので、Jekyllの公式サイトから無料で使用できるテーマをダウンロードしたいと思います。
公式サイトを見ると有料と無料の色々なテーマがありますが、 今回は[ブログ用のテーマ](https://jekyllthemes.io/jekyll-blog-themes){:target="_blank"}から無料のものを選択肢します。
私は [Scriptor](https://jekyllthemes.io/theme/scriptor){:target="_blank"} というなかなかイケてるテーマがあったのでそれにしました。

```
$ cd ~/     //ホームディレクトリに移動（これは好きな場所でOK）
$ git clone https://github.com/JustGoodThemes/Scriptor-Jekyll-Theme.git
$ bundle exec jekyll serve
```
http://localhost:4000 にアクセスして以下のようにテーマが反映されている事を確認します。

![scriptor_template](2020-05-24/images/scriptor_template.png)

試しにマークダウンファイルを作成して自分でも記事が作成出来る事を確認しましょう。

以下ディレクトリ配下に2020-01-01-test.mdというマークダウンファイルを作成
/Users/kankimura/Scriptor-Jekyll-Theme/_posts

以下内容を記述して保存
```
---
layout: post
title: "test"
description: "test"
date: 2020-01-01
---
テストですよ。
```
http://localhost:4000 を更新すると作成した記事が反映されていることが分かります。

![test-article](2020-05-24/images/test-article.png)

今後記事を作成するする際はこのようにマークダウンファイルを作成してローカルで確認後にGitHubPagesにアップして公開する流れになります。

このままだとダウンロードしたままの情報が残ってしまいますので最低限以下は変更しておきましょう。

不要なマークダウンファイルを削除
筆者情報を変更
/Users/kankimura/Scriptor-Jekyll-Theme/_data/author.json
不要なSNS情報を削除
/Users/kankimura/Scriptor-Jekyll-Theme/_data/social.json
Aboutページの編集
/Users/kankimura/Scriptor-Jekyll-Theme/about.md

 ### GitHub Pagesへ公開

 #### GitHubアカウントの作成

 ### Gitのインストール

 ### リポジトリの作成

 ### GitHub Pagesへ公開

 


参考
http://jmcglone.com/guides/github-pages/
https://jekyllrb.com/docs/
https://marbles.hatenablog.com/entry/2019/01/16/221417
https://qiita.com/stkdev/items/0e2df27736acbea9bd26

・リポジトリの削除
https://qiita.com/PlanetMeron/items/4d164eff7bff2243cf06

・テーマを適用する方法
https://howpon.com/10476

今後やってみたい事
・コメントフォームの実装
http://kikei.github.io/
https://www.kooslooijesteijn.net/blog/comments-system-for-static-website
https://www.talkyard.io/plans
->talkyardは月1.9ユーロという値段で使えるので良さそう


・gitの最低限の使用方法

git init：ローカルリポジトリを作成する
git add：対象ファイルをコミット対象に追加する
git commit：対象ファイルをコミットする
git remote add <name> <url>:リモートリポジトリのurlに名称を付ける。
　（これによってpushする際にurlを記述しなくてよくなる。）
　URL:git@github.com:<username>/<repo-name>.git
git push　<name> master:リモートリポジトリのマスターブランチにプッシュにコミットを反映する

git checkout：ブランチを切り替える
git merge
