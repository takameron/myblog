---
title: "Slackのメッセージをバックアップ"
date: 2021-10-02T11:57:00+09:00
lastmod: 2021-10-02T11:57:00+09:00
author: "たかめろん"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1632994946/Blog-personal/slack_dump/thumbnail.png"]
categories: ["ソフトウェア・サービス"]
tags: []
archives: ["2021","2021-10"]
toc: true
draft: false
---

Slackにおける自分が閲覧できる範囲のチャンネルやDMをJSON形式でダウンロードできる、slack-dumpというソフトウェアがあります。
[フォーク履歴](https://github.com/joefitzgerald/slack-dump/network/members "joefitzgerald/slack-dump: Export History For Private Groups From Slack")を見ると、初出は2015年、その後たくさんフォークされてそれぞれ改良が加えられています。

2021年になり、slack-dumpで使っているSlackのAPIに大きな変更がありました。
この変更に追従できていないリポジトリは多く、slack-dumpが使えない状況となっていました。
というわけで、私のほうでフォークして、APIに合わせて大幅に書き換え、2021年現在最新の状態にしました！

こちらがリポジトリです。
{{< blogcard "https://github.com/takameron/slack-dump" >}}

安全性が心配でしたら、すべての処理が```main.go```に書かれていますのでご確認ください。
とはいっても、SlackのAPIと実際に通信するパッケージのメソッドを呼んでデータを持ってきて、ファイルに書き込んで圧縮ファイルを作るだけですが…

[リリースページ](https://github.com/takameron/slack-dump/releases "Releases · takameron/slack-dump")から実行ファイルをダウンロードできます。

## 実行方法
実行方法はリポジトリのREADME.mdに書かれていますが、こちらでも紹介します。

### Tokenの取得
まずはSlackのAPIを使うためにTokenを取得します。
Tokenはワークスペースに導入するアプリを作成することで生成できます。

[https://api.slack.com/](https://api.slack.com/)にアクセスし、「Create an app」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1633137989/Blog-personal/slack_dump/1.png" alt="APIのポータルページ" caption="APIのポータルページ" >}}

以下の画面が表示された場合は「Create an app」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1633138557/Blog-personal/slack_dump/2.png" alt="所有アプリ一覧画面" caption="所有アプリ一覧画面" >}}

「From scratch」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1633137989/Blog-personal/slack_dump/3.png" alt="アプリ作成画面" caption="アプリ作成画面" >}}

アプリ名と、どのワークスペースに導入するかを指定します。アプリ名は何でもよく、ワークスペースはバックアップしたいワークスペースを選んでください。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1633137989/Blog-personal/slack_dump/4.png" alt="アプリ名と導入するワークスペースの指定画面" caption="アプリ名と、どのワークスペースに導入するかを指定" >}}

左側にある「Oauth & Permissions」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1633137988/Blog-personal/slack_dump/5.png" alt="サイドバーに「Oauth & Permissions」がある" caption="権限管理ページに移動" >}}

スクロールしていくと、以下の画面になります。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1633137989/Blog-personal/slack_dump/6.png" alt="スコープの設定画面" caption="スコープの設定画面" >}}

「User Token Scopes」の欄に以下のスコープを追加します。

* channels:read
* channels:history
* groups:read
* groups:history
* im:read
* im:history
* mpim:read
* mpim:history
* users:read

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1633137988/Blog-personal/slack_dump/7.png" alt="スコープを設定後" caption="スコープを設定後" >}}

ページの上部に戻り、「Install to Workspace」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1633137988/Blog-personal/slack_dump/8.png" alt="アプリのインストール" caption="アプリのインストール" >}}

許可を求められるので、「Allow」をクリックして許可します。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1633137988/Blog-personal/slack_dump/9.png" alt="権限の許可を求める画面" caption="権限を許可する" >}}

Tokenが表示されます。これはプログラムで使うので、コピーしておいてください。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1633141666/Blog-personal/slack_dump/10.png" alt="Tokenの表示画面" caption="「User OAuth Token」をコピー" >}}

### Macで実行
Macでの実行方法を説明します。
まず、GitHubからダウンロードしてきただけでは実行権限がないので、以下のコマンドで実行権限を付与します。

```[ファイル名]```のところは実際のファイル名（例：slack-dump_1.3.0_Darwin_x86_64）にしてください。

```text {linenos=false}
chmod +x [ファイル名]
```

実行します。

```text {linenos=false}
./[ファイル名]
```

Appleの公証を受けていないため実行をブロックされます。このプログラムを使いたい場合は「キャンセル」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1633138566/Blog-personal/slack_dump/mac1.png" alt="slack-dumpの実行ブロック画面" caption="slack-dumpの実行をブロックされた" >}}

このプログラムを信頼していただけるなら、実行をブロックされたあとに「システム環境設定」→「セキュリティとプライバシー」→「一般」の画面から実行を許可できます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1633137989/Blog-personal/slack_dump/mac2.png" alt="システム環境設定の「セキュリティとプライバシー」の画面" caption="実行を許可する" >}}

## おわり
大事な会話・消えては困る会話がたくさんある時に、JSON形式で見づらいですが手元に残せますので、ぜひご利用ください。
