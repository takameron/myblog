---
title: "MiniTool Partition Wizardでパーティション編集"
date: 2020-12-06T11:26:00+09:00
lastmod: 2020-12-06T11:26:00+09:00
author: "たかめろん"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1607170180/Blog-personal/minitool_partition_wizard/main.png"]
categories: ["ソフトウェア・サービス"]
tags: ["レビュー"]
archives: ["2020", "2020-12"]
toc: true
draft: false
---

Windowsでパーティションを編集しようとすると、標準機能（「ディスクの管理」）は使いにくいです。
LinuxをDVDからブートして、GPartedを使っているのは私だけでしょうか？（笑）

今回は『MiniTool Partition Wizard 無料版』の紹介を頂きましたので使ってみました！  

{{< blogcard "https://www.partitionwizard.jp/" >}}
[英語版Webページ](https://www.partitionwizard.com/ "MiniTool Partition Wizard | Best partition magic alternative for Windows PC and Server")

{{< warning >}}
本記事はレビュー記事です。記事依頼を受け、「MiniTool Partition Wizard プロ・デラックス版」の提供を受けています。
{{< /warning >}}

**今回はバージョン12.1を使用しています。本記事の情報は古くなっている可能性にご注意ください。**

Windows向けのディスク管理ソフトウェアで、無料版が提供されています。
無料版の機能の一部を紹介すると、パーティションの結合・分割・拡張・フォーマット・抹消、さらにファイルシステムのエラーチェックと修復ができます。
ここまでできれば、日常的に出くわす場面では困りませんね！
詳しくは[エディションの比較](https://www.partitionwizard.jp/comparison.html "MiniTool Partition Wizard バージョン別機能一覧")をご確認ください。

対応しているフォーマット方式は以下の通りです。

* FAT12/16/32
* exFAT
* NTFS
* ext2/3/4

Windowsで使われるフォーマットに加えて、ext2/3/4にも対応しているのが良いですね！

## 感想
まずは使ってみた感想です。

### たくさんの機能がある

[エディションの比較](https://www.partitionwizard.jp/comparison.html "MiniTool Partition Wizard バージョン別機能一覧")を見ると（[機能](#機能)の章でも紹介しています）、無料版でもたくさんの機能があります。
また、コンテキストメニュー（右クリックメニュー）にもたくさんの選択肢があります（いくつかは有料版限定ですが…）。
思い立った時にサクッとパーティションを編集できるように、とりあえずいろいろな機能があるソフトウェアを1つ持っておくのは良さそうです。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170180/Blog-personal/minitool_partition_wizard/right_click.png"  alt="コンテキストメニューを表示した画面" caption="たくさんの機能" >}}

### UIがキレイ

機能はたくさんありますが、UIは見やすくまとまっています。
初見かつ一発で目的の機能を呼び出すのはこのようなUIに慣れていないと難しいかもしれません。
しかし、初心者でもそれほど迷うことなく使えそうです。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170180/Blog-personal/minitool_partition_wizard/main.png"  alt="メイン画面" caption="メイン画面" >}}

### ヘルプが充実している

こちらにオンラインマニュアルがあり、スクリーンショットも使いながらわかりやすく解説されています。

{{< blogcard "https://www.partitionwizard.jp/help/" >}}

さらにウィザードには、ウィンドウの下部にチュートリアル（機能の説明）へのリンクが載っています。
これをクリックするだけで、どんなことをする機能なのかや画面の操作方法を知ることができます。
ドキュメントが充実していて利用者に優しいですね。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607173509/Blog-personal/minitool_partition_wizard/tutorial.png"  alt="ヘルプへのリンク" caption="ヘルプへのリンク" >}}

### サポートが充実

なんとビックリ、無料版にもメールでの技術サポートがあります！
日本語にも対応しています。

{{< blogcard "https://www.partitionwizard.jp/support.html" >}}

まずはオンラインマニュアルを確認し、それでも困ったことがあれば技術サポートに相談するのが良さそうです。
これは嬉しいですね。

### 気になる点
* 公式サイトの日本語がやや不自然

言い回しがおかしかったり、誤字脱字が見受けられます。
[会社概要](https://www.partitionwizard.jp/about-us.html "MiniToolについて")を見ると、カナダと香港に拠点を構える会社のようです。
さらにインストール時の言語選択では7言語から選べますので、おそらく他言語から翻訳したのでしょう。
むしろ日本語対応しているのが日本人としてありがたい！
ただ、不審感がありもったいないので、改善していただきたいですね…

* 実際にメニューを選択しないと無料版で使える機能かどうかがわからない

実際に機能をクリックすると、それが有料版限定の機能だった場合に以下の画面が表示されます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170182/Blog-personal/minitool_partition_wizard/upgrade.png"  alt="アップグレードのおすすめ" caption="アップグレードのおすすめ" >}}

クリックしたあとにこれが表示されると、なんだか残念な気持ちになります（笑）
機能を選択できないようになっていたらわかりやすいのに…

とはいえ、全体的には無料でここまで使えるのは素晴らしいです。

## 機能
[こちら](https://www.partitionwizard.jp/comparison.html "MiniTool Partition Wizard バージョン別機能一覧")から無料版の機能を抜粋してみました。
パーティションの編集はひととおりのことができ、さらにメタデータの設定や抹消機能があります。

### 新機能
* ディスクベンチマーク
* ディスク使用状況分析

### パーティション変更
* パーティション
	- 移動/サイズ変更
	- 拡張
	- 結合
	- 分割
	- プライマリに設定
	- 論理に設定
* FATをNTFSに変換

### パーティション管理
* パーティション
	- 新規作成
	- 削除
	- フォーマット
	- アライメント
	- 抹消
	- アクティブ/非アクティブに設定	
	- ラベル名をつける
	- ドライブ文字変更
	- 表示/非表示
* 非OSパーティション コピー

### パーティション検査検出
* ファイルシステムエラー検出と修復
* パーティション一覧	
* サーフェス テスト（不良セクタの検出）
* パーティション プロパティ一覧

### ディスク変換
* データディスクをMBR/GPTに変換

### ディスク複製
* 非OSディスク コピー

### ディスク抹消
* ディスク抹消
* すべてのパーティションを削除

### ディスク検査検出
* すべてのパーティションをアライメント
* MBR再構築
* サーフェステスト
* 紛失/削除したパーティションを検出（復元はできない）
* ディスク プロパティ


## インストール
[こちら](https://www.partitionwizard.jp/free-partition-manager.html "無料パーティション管理ソフト - MiniTool Partition Wizard 無料版")からダウンロードします。
ダウンロードした実行ファイルをダブルクリックして起動します。

ユーザーアカウント制御の画面が表示されるので、問題ないソフトウェアだと判断したら「はい」を選択してください。

言語の選択では、日本語を選択します。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170179/Blog-personal/minitool_partition_wizard/1.png"  alt="言語選択" caption="言語選択" >}}

2種類のソフトウェアがバンドルされています。
パーティション編集だけをしたい場合は、「MiniTool ShadowMaker Free」のチェックを外してください。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170180/Blog-personal/minitool_partition_wizard/2.png"  alt="製品の選択" caption="製品の選択" >}}

インストール先の指定では、通常はそのままで大丈夫です。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170180/Blog-personal/minitool_partition_wizard/3.png"  alt="インストール先の指定" caption="インストール先の指定" >}}

インストールが始まります。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170180/Blog-personal/minitool_partition_wizard/4.png"  alt="インストール中" caption="インストール中" >}}

インストールが完了しました。
チェックを入れたまま「完了」ボタンを押すと、ソフトウェアが起動します。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170180/Blog-personal/minitool_partition_wizard/5.png"  alt="インストール完了" caption="インストール完了" >}}

このソフトウェアは起動するたびにユーザーアカウント制御の画面が表示されます。
パーティションを編集するという大きな権限を必要とするソフトウェアですので、ソフトウェアの機能的にユーザーアカウント制御が表示されるのは不思議ではありません。

## ディスクのエラーチェック
とりあえず、必要に迫られて行うであろうディスクのエラーチェックを試してみます。

チェックしたいパーティションを右クリックして、コンテキストメニューから「ファイルシステムチェック」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170181/Blog-personal/minitool_partition_wizard/fc1.png"  alt="コンテキストメニュー" caption="「ファイルシステムチェック」をクリック" >}}

オプションを設定して「開始」ボタンをクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170180/Blog-personal/minitool_partition_wizard/fc2.png"  alt="「ファイルシステムチェック」ウィザード　チェック開始" caption="チェックの開始" >}}

しばらくすると、結果が表示されます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170180/Blog-personal/minitool_partition_wizard/fc3.png"  alt="「ファイルシステムチェック」ウィザード　チェック完了" caption="チェックの完了" >}}

迷うことなく操作できますね。

## パーティションの分割
パーティションの分割をやってみます。

分割したいパーティションを右クリックして、コンテキストメニューから「分割」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170182/Blog-personal/minitool_partition_wizard/separate1.png"  alt="コンテキストメニュー" caption="「分割」をクリック" >}}

新しいパーテンションのサイズをスライドさせて指定します。
直感的に操作できます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170183/Blog-personal/minitool_partition_wizard/separate2.png"  alt="分割サイズの設定" caption="分割サイズの設定" >}}

テキストボックスに直接入力することもでき、単位を変更することもできます。
指定したら「OK」ボタンをクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170182/Blog-personal/minitool_partition_wizard/separate3.png"  alt="分割サイズの設定" caption="単位を切り替えられる" >}}

この画面に戻ったら、左下の「適用」ボタンをクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607214038/Blog-personal/minitool_partition_wizard/separate4.png"  alt="操作実行前" caption="「適用」をクリック" >}}

確認ウィンドウが表示されます。
パーティションの変更処理中にデータを保存するような処理を行うとトラブルとなる可能性があります。極力他のソフトウェアは終了しておくのが良いです。  
他のソフトウェアをひととおり終了したら「はい」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170182/Blog-personal/minitool_partition_wizard/separate5.png"  alt="確認ウィンドウ" caption="確認" >}}

パーティションの変更処理が始まります。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170182/Blog-personal/minitool_partition_wizard/separate7.png"  alt="処理中" caption="処理中" >}}

処理が完了しました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170182/Blog-personal/minitool_partition_wizard/separate8.png"  alt="完了" caption="完了" >}}

簡単ですね。

## パーティション抹消
パーティションの抹消も、以下のように簡単な操作で実行できます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607221197/Blog-personal/minitool_partition_wizard/erase.png"  alt="パーティションの抹消" caption="パーティションの抹消" >}}

ちなみに、データを消す手段には「削除」と「抹消」があります。
削除と抹消の違いは、削除は管理データを消すだけ、抹消はデータ領域に上書きをするという違いがあります。つまり、削除ではデータ本体は残っているため、復元される可能性があります。
ドライブを捨てるときは、削除ではなく抹消を行う必要があります。

## ディスク使用状況
パーティションをいじっていると、「空き容量が少ないけれど、いったいなぜ？」と思うことがあります。
そこで、フォルダやファイルのディスク使用割合を見られる「ディスク使用状況分析」が便利です。

上部の「ディスク使用状況分析」をクリックし、「スキャン」ボタンを押すと分析が始まります。

結果は以下のように表示されます。
かゆいところに手が届いて便利ですね。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1607170182/Blog-personal/minitool_partition_wizard/usage.png"  alt="ディスク使用状況分析" caption="ディスク使用状況分析" >}}

## まとめ
多彩な機能を持つ『MiniTool Partition Wizard 無料版』を紹介しました。

以下からダウンロードできます。

{{< blogcard "https://www.partitionwizard.jp/free-partition-manager.html" >}}

また、有料版では使える機能が多くなっています。
機能や価格は以下から見ることができます。

{{< blogcard "https://www.partitionwizard.jp/comparison.html" >}}
