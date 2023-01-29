---
title: "MiniTool ShadowMakerで簡単バックアップ管理"
date: 2023-01-29T01:57:05+09:00
lastmod: 2023-01-29T20:51:50+09:00
author: "たかめろん"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1674907591/Blog-personal/minitool_shadow_maker/4.png"]
categories: ["ソフトウェア・サービス"]
tags: ["レビュー", "バックアップ"]
archives: ["2023","2023-01"]
toc: true
draft: false
---

新年、学生の方は卒論や修論、また年度末に向けて各種報告書などを作成する方も多いのではないでしょうか。
みなさん、バックアップは取っていますか！
いつパソコンが壊れるかわかりません。
パソコンが壊れて代替機は用意できても、データも消失してしまえば、作り直しという膨大な手間と時間がかかります。
新年が始まったばかりのこのタイミングで、データ消失対策を考えてみてはいかがでしょうか。
[バックアップ](https://jp.minitool.com/backup/system-backup.html)は大切です。

今回は『MiniTool ShadowMaker 無料版』の紹介を頂きましたので使ってみました！  
MiniTool ShadowMakerはバックアップソフトで、バックアップや同期、さらにディスクのクローンなどの機能があります。

{{< blogcard "https://jp.minitool.com/backup/system-backup.html" >}}
[英語版Webページ](https://www.minitool.com/backup/system-backup.html "Best Free Backup Software for Windows | MiniTool ShadowMaker")

{{< warning >}}
本記事はレビュー記事です。記事依頼を受け、「MiniTool ShadowMakerプロ・アルティメット版（１台ｐｃ用）」の提供を受けています。
{{< /warning >}}

**今回はバージョン4.0.3を使用しています。本記事の情報は古くなっている可能性にご注意ください。**

## ダウンロードとインストール

[無料版のダウンロードページ](https://jp.minitool.com/backup/system-backup.html)を開き、「無料ダウンロード」ボタンをクリックします（2023年1月28日現在）。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674908593/Blog-personal/minitool_shadow_maker/download.png"  alt="ダウンロードページに「無料ダウンロード」ボタンと「Proにアップグレード」ボタンが表示されている" caption="ダウンロードページ" >}}

ダウンロードしたファイルをダブルクリックし、インストーラを起動します。

「今すぐインストール」ボタンをクリックしてインストールを開始します。
{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907585/Blog-personal/minitool_shadow_maker/1.png"  alt="「今すぐインストール」ボタンがある" caption="インストーラの起動画面" >}}

しばらく待ちます。
{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907586/Blog-personal/minitool_shadow_maker/2.png"  alt="インストールが進行中で、プログレスバーが表示されている" caption="インストール中" >}}

インストールが完了したので、「今すぐ開始」をクリックします。
{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907586/Blog-personal/minitool_shadow_maker/3.png"  alt="「インストールが完了　今すぐコンピュータをバックアップしましょう。」を表示されている" caption="インストール完了" >}}

## 言語切り替え

この記事では英語表示のまま使っていますが、日本語表示にも対応しています！

まずは右上にある横棒3本のところをクリックし、「Language」→「Japanese」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674916226/Blog-personal/minitool_shadow_maker/language.png"  alt="ウィンドウの右上のハンバーガーメニューから、「Language」→「English」にチェックが入っている" caption="Japaneseを選択" >}}

表示されるメッセージの通り、ソフトウェアを終了させ、再び起動します。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674916226/Blog-personal/minitool_shadow_maker/language2.png"  alt="「Please restart application to apply the selected language.」と表示されている" caption="「選択した言語を適用するためにアプリケーションを再起動してください」のメッセージ" >}}

日本語表示になりました！

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674916355/Blog-personal/minitool_shadow_maker/language3.png"  alt="日本語表示のツール画面" caption="全体が日本語化されています" >}}

## 機能

どのような機能があるのか、ざっと見ていきます！👀

まずはホーム画面。PCの情報や、前回・次回のバックアップの情報などを見られるようです。
（ところで、Windows11のパソコンで試していますが、Windows10だと認識されていますね…）

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907585/Blog-personal/minitool_shadow_maker/Home.png"  alt="ホーム画面" caption="Home" >}}

バックアップ画面。バックアップ元とバックアップ先は、大きなボタンを押して、簡単に選べるようになっています。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907585/Blog-personal/minitool_shadow_maker/Backup.png"  alt="バックアップ画面" caption="Backup" >}}

同期画面。バックアップ機能との違いは、同期機能だと同期元のファイルやフォルダの削除も同期先に反映されます。
つまり、昔に消してしまったファイルを復元したいという用途には使えません。
しかし、不要なファイルがバックアップ先に貯まり、容量を圧迫するという事態を防げます。

突然パソコンが壊れた時にデータを残しておきたいだけなら同期機能で十分ですし、昔に消したファイルを復元したいかもしれなかったらバックアップ機能が必要など、目的に応じてバックアップ機能と同期機能を使い分けてください。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907587/Blog-personal/minitool_shadow_maker/Sync.png"  alt="同期画面" caption="Sync" >}}

復元画面。バックアップしたことがあれば、それを復元できます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907588/Blog-personal/minitool_shadow_maker/Restore.png"  alt="復元画面" caption="Restore" >}}

管理画面。「実行中のすべてのバックアップが完了したらパソコンをシャットダウンするか」というチェックボックスがあります。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907586/Blog-personal/minitool_shadow_maker/Manage.png"  alt="管理画面" caption="Manage" >}}

ログ画面。バックアップや同期を実行すると、実行履歴が表示されます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907586/Blog-personal/minitool_shadow_maker/Logs.png"  alt="ログ画面" caption="Logs" >}}

ツール画面。「メディアビルダー」（ディスクが故障して起動できなくなった時に起動する用）、「ブートメニューの追加」（MiniToolリカバリ環境用のWindowsスタートアップメニューを追加）、「マウント解除」（ディスクやUSBメモリなどの取り外し）、「ディスクのクローン」（ディスク全体を、他のディスクにコピーする）などの機能があります。
バックアップ機能や同期機能だけでは物足りない場合は、こちらも確認しておくと良さそうです。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907590/Blog-personal/minitool_shadow_maker/Tools.png"  alt="ツール画面" caption="Tools" >}}

## Syncを試してみる

同期機能を使ってみます！

まずは「SOURCE」（同期元）のフォルダを選択します。
左側の大きなボタンをクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907587/Blog-personal/minitool_shadow_maker/Sync.png"  alt="同期画面" caption="Sync" >}}

今回は「卒業論文」というフォルダを同期してみます
（大学生のみなさん、卒論のバックアップはこまめに取りましょう！
大学4年間ずっと同じパソコンを使っていれば、いつ寿命を迎えてもおかしくありません！）。

フォルダを選択したら、「OK」ボタンをクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907589/Blog-personal/minitool_shadow_maker/Sync1.png"  alt="同期元のフォルダを選択" caption="同期元のフォルダを選択" >}}

フォルダのパスと、フォルダ内にあるファイルの総容量を確認できます。

次は「DESTINATION」（同期先）のフォルダを選択します。
右側の大きなボタンをクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907588/Blog-personal/minitool_shadow_maker/Sync2.png"  alt="「SOURCE」にフォルダ名とパスが表示された同期画面" caption="" >}}

今回はUSBメモリ（ここではDドライブ）に同期します。
同期先を選択して、「OK」ボタンをクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907589/Blog-personal/minitool_shadow_maker/Sync3.png"  alt="同期先のフォルダを選択" caption="同期先のフォルダを選択" >}}

これで、同期元と同期先を選択し終わりました！
ちょっと「Options」を覗いてみます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907588/Blog-personal/minitool_shadow_maker/Sync4.png"  alt="「SOURCE」と「DESTINATION」にフォルダ名とパスが表示された同期画面" caption="" >}}

どの項目を見てファイルが更新されているの判定をするのか、の設定があります。
「ファイル更新日時」「ファイルサイズ」「ファイル内容」のうち、少なくとも1つを選択しておく必要があるそうです。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907589/Blog-personal/minitool_shadow_maker/Sync5.png"  alt="Optionsの「File Sync Options」内の「Comparison」設定" caption="比較項目" >}}

除外するファイル形式の設定もあります。
バックアップファイルや一時ファイル、勝手に作られるファイルやごみ箱フォルダなど、同期する必要がないものを除外することができます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907590/Blog-personal/minitool_shadow_maker/Sync6.png"  alt="Optionsの「File Sync Options」内の「Filter」設定" caption="除外するファイル" >}}

さて、同期画面に戻り、同期を開始してみます。
同期を後で実行するボタンと、今すぐ実行するボタンがあります。
ここでは「Sync Now」をクリックし、今すぐ同期を開始します。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907590/Blog-personal/minitool_shadow_maker/Sync7.png"  alt="「Sync Now」にカーソルを合わせた同期画面" caption="同期開始" >}}

処理が始まりました。プログレスバーで進捗がわかります。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907590/Blog-personal/minitool_shadow_maker/Sync9.png"  alt="同期中でプログレスバーが表示されている" caption="同期中" >}}

処理が完了しました！

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907587/Blog-personal/minitool_shadow_maker/Sync10.png"  alt="同期が完了した" caption="同期完了" >}}

エクスプローラーで、同期先（ここではUSBメモリ）の中身を見てみます。

見慣れないフォルダが作成されています。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907587/Blog-personal/minitool_shadow_maker/Sync11.png"  alt="エクスプローラーで同期先を開いた画面" caption="同期先に作成されたフォルダ" >}}

開いてみると、見知らぬファイルの中に、同期した「卒業論文」フォルダがありました！
中身も、同期元とそのままです。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1674907587/Blog-personal/minitool_shadow_maker/Sync12.png"  alt="エクスプローラーで同期先にできたフォルダを開いている画面" caption="同期先に同期元のフォルダがある" >}}

## 感想

雑感を書いていきます。

### 操作しやすい画面

1画面あたりのボタンの数が少なく、ボタンも文字も大きく、見やすくて操作しやすいです。

ツール系のソフトでは、たくさんのボタンや入力欄があって操作に困るようなUIのものも多くあります。
このソフトは自分で理解しやすく、また他人に操作方法を教えるときにも、伝えやすそうです。

### ファイルがそのままコピーされる

Sync（同期）機能を試したところ、同期先には同期元のファイルがそのままありました。
バックアップソフトによっては独自形式で圧縮されることもあり、そうするとそのソフトがないと復元できません。
フォルダをそのままコピーしてくれると、いざ緊急事態が発生したときに、わざわざバックアップソフトをインストールしなくても、エクスプローラーでコピーして復元することが可能です。
特定のソフトウェアに依存しなくても復元できるのは重要なポイントだと思います。

### 無料版でもそれなりに使える

このソフトウェアには複数のグレードがありますが、下記サイトで相違点を見ると、無料版でも基本機能はチェックマークがついており、バックアップソフトとしてはさほど困ることなく使えそうです。

{{< blogcard "https://jp.minitool.com/backup/backup-software-comparison.html" >}}

また、ディスクのクローン機能が使えるので、新しいディスクに換装する時に便利そうなのがいいですね。
（クローンしたディスクでWindowsが起動するかなどは手元で確認していません 🙇 [Webページ](https://jp.minitool.com/backup-tips/create-bootable-usb-from-iso.html#%E6%8F%90%E6%A1%88%EF%BC%9Awindows%E3%82%92%E3%83%90%E3%83%83%E3%82%AF%E3%82%A2%E3%83%83%E3%83%97%EF%BC%86%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0%E3%82%92%E5%BE%A9%E5%85%83-174)を見る感じだと使えそうです ）

---

『MiniTool ShadowMaker 無料版』という[バックアップソフト](https://jp.minitool.com/backup/system-backup.html)を紹介しました。

以下からダウンロードできます。

{{< blogcard "https://jp.minitool.com/backup/system-backup.html" >}}

データを失う前に、データをどう守るか、検討してみることをおススメします。
