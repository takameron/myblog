---
title: "ブラウザでのダウンロードに失敗する時の対処法"
date: 2019-09-19T00:53:00+09:00
lastmod: 2019-09-19T00:53:00+09:00
author: "ぶっち"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1580349280/Blog-personal/download_failed/download_failed.png"]
categories: ["Tips"]
tags: []
archives: ["2019", "2019-09"]
toc: true
draft: false
---

ブラウザで大きなファイルをダウンロードしようとすると、ダウンロードに失敗してしまうことがあります。
ちょうど私もRaspbian（Raspberry PiのOS）をブラウザでダウンロードしようとして失敗しています。  
そこで、これを題材に対処法をご紹介したいと思います。

私が思いつく対処法は、以下の3点です。

1. ミラーサイトを探す
1. wgetコマンドを使う
1. 時間をおく

すぐに理解された方もいらっしゃると思いますが、順に説明していこうと思います。

## ミラーサイトを探す
海外のサーバからファイルをダウンロードすると、遠くから海を渡って、いろいろなサーバを経由してデータが届くため、どうしても遅くなりやすいです。
ところが有名なファイル(Linux系OSのイメージファイルやCygwinのパッケージファイルなど)だと、日本国内にファイルをコピーして配信してくださっている場合があります。

このように日本国内にミラーサイトがある場合、海外からダウンロードする場合に比べて、 *高速* なダウンロードが可能です。
まずは、ミラーサイトがないか、検索してみてください。

### 注意！
ミラーサイトなどの正規でないサーバからダウンロードする場合、マルウェアが混入されるなど、ファイルが *改ざん* されている恐れがあります。

*ファイルが改ざんされていないか確かめるためには、ハッシュ値の比較を行います。*  
ファイルのダウンロードリンクの近く、または別途テキストファイルに、以下の「SHA-256」に続く英数字のようなものが記載されていることが多いです。
この英数字をハッシュ値といい、ファイルごとに固有の文字列になります。
また、「SHA-256」はハッシュ関数といい、ハッシュ値を計算するアルゴリズムの名前です。
ハッシュ関数はいくつか種類があり、ハッシュ関数ごとにハッシュ値は異なります。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580349280/Blog-personal/download_failed/hash_num.png"  alt="ハッシュ値が書かれたダウンロードページ" caption="ハッシュ値はどこかに書かれています" >}}

ハッシュ値の比較方法は、以下の手順になります。

1. ダウンロードしたファイルのハッシュ値を得る
1. 公式サイトに記載されているハッシュ値と比較する

ハッシュ値を得るツールはさまざまなものがあります。
自身のOSにあったハッシュ値を計算するソフトウェアを、検索サイトで検索してみてください。
MacやLinuxでは、ハッシュ値を計算するコマンドがあります。

まず、何らかのツールを使って、ダウンロードしたファイルのハッシュ値を得ます。
まずは、公式サイトに記載されているハッシュ値が、どのハッシュ関数が使われたかを確認します。
同じハッシュ関数で、手元のファイルのハッシュ値を確認してください。

次に、公式サイトに記載されているハッシュ値と、求めたばかりのハッシュ値を比較します。
一致していれば、そのファイルは公式サイトのファイルと同一であると考えて問題ありません。
しかし、一致していなければ、ハッシュ関数が違うか、または公式サイトで配布しているファイルとは異なることがわかります。
一致していない理由がわかっているならば良いですが、一致すべきはずなのに一致していない場合は、そのファイルは危険だと考えられます。

正規でないサーバからのダウンロードは、安易に信用すべきでありません。  
*必ずハッシュ値の確認を！*

### 例
Raspbianのダウンロードを、公式サイトとJAISTのミラーサイトの両方から行ってみましたので、その様子を比較しようと思います。
wgetコマンドを使った様子は、下の方に貼り付けてあります。
また、私が様子を観察した結果をもとに、評価しています。

国内サーバの方が、以下の点で優位でした。

* ダウンロード速度が早い
* リトライ数が少ない

ダウンロード速度は刻一刻と大きく変わるので単純な比較はできませんが、以下に一例を示します。
観察した様子だと、全体的に国内のミラーサイトの方が速度が速かったです。

|  公式  |  ミラー  |
| :----: | :----: |
| 23KB/s | 122KB/s |

wgetコマンドでダウンロードを行うと、ダウンロードに失敗したときに途中から再開する機能があります。
以下に、全てをダウンロードし終わるまでのダウンロード回数を示します。
国内のミラーサイトの方がダウンロードに失敗する回数が少なく、安定していることがわかります。

| 公式 | ミラー |
| :--: | :--: |
| 7回  | 2回  |

私の場合は、公式サイトからのダウンロード開始から数分後に国内のミラーサイトからのダウンロードを開始したにもかかわらず、国内のミラーサイトからの方が圧倒的な差をつけて先にダウンロードが完了しました。

国内のミラーサイトが使えるならば、信頼できるミラーサイトからダウンロードするのがオススメです。

公式（海外）
```plain
C:\Users\user>wget https://downloads.raspberrypi.org/raspbian_latest
--2019-09-18 21:24:49--  https://downloads.raspberrypi.org/raspbian_latest
Resolving downloads.raspberrypi.org (downloads.raspberrypi.org)... 93.93.130.104, 93.93.130.39, 93.93.135.188, ...
Connecting to downloads.raspberrypi.org (downloads.raspberrypi.org)|93.93.130.104|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://downloads.raspberrypi.org/raspbian/images/raspbian-2019-07-12/2019-07-10-raspbian-buster.zip [following]
--2019-09-18 21:24:51--  https://downloads.raspberrypi.org/raspbian/images/raspbian-2019-07-12/2019-07-10-raspbian-buster.zip
Connecting to downloads.raspberrypi.org (downloads.raspberrypi.org)|93.93.130.104|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1152275926 (1.1G) [application/zip]
Saving to: 'raspbian_latest'

raspbian_latest                 2%[>                                               ]  25.41M  12.9KB/s    in 5m 47s

2019-09-18 21:30:40 (74.9 KB/s) - Read error at byte 26640384/1152275926 (The TLS connection was non-properly terminated.). Retrying.

--2019-09-18 21:30:41--  (try: 2)  https://downloads.raspberrypi.org/raspbian/images/raspbian-2019-07-12/2019-07-10-raspbian-buster.zip
Connecting to downloads.raspberrypi.org (downloads.raspberrypi.org)|93.93.130.104|:443... connected.
HTTP request sent, awaiting response... 206 Partial Content
Length: 1152275926 (1.1G), 1125635542 (1.0G) remaining [application/zip]
Saving to: 'raspbian_latest'

raspbian_latest                 7%[+=>                                             ]  77.66M  45.0KB/s    eta 6h 20m
```

ミラー（国内）
```plain
C:\Users\user\Downloads>wget http://ftp.jaist.ac.jp/pub/raspberrypi/raspbian/images/raspbian-2019-07-12/2019-07-10-raspbian-buster.zip
--2019-09-18 21:30:31--  http://ftp.jaist.ac.jp/pub/raspberrypi/raspbian/images/raspbian-2019-07-12/2019-07-10-raspbian-buster.zip
Resolving ftp.jaist.ac.jp (ftp.jaist.ac.jp)... 150.65.7.130
Connecting to ftp.jaist.ac.jp (ftp.jaist.ac.jp)|150.65.7.130|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1152275926 (1.1G) [application/zip]
Saving to: '2019-07-10-raspbian-buster.zip'

2019-07-10-raspbian-buster.zi   5%[=>                                              ]  62.50M   190KB/s    in 5m 16s

2019-09-18 21:35:49 (203 KB/s) - Connection closed at byte 65537530. Retrying.

--2019-09-18 21:35:50--  (try: 2)  http://ftp.jaist.ac.jp/pub/raspberrypi/raspbian/images/raspbian-2019-07-12/2019-07-10-raspbian-buster.zip
Connecting to ftp.jaist.ac.jp (ftp.jaist.ac.jp)|150.65.7.130|:80... connected.
HTTP request sent, awaiting response... 206 Partial Content
Length: 1152275926 (1.1G), 1086738396 (1.0G) remaining [application/zip]
Saving to: '2019-07-10-raspbian-buster.zip'

2019-07-10-raspbian-buster.zi  26%[++=========>                                    ] 295.07M   113KB/s    eta 51m 47s
```

## wgetコマンドを使う
wgetコマンドは、ダウンロードを行うコマンドです。
非常に高機能なコマンドですが、機能のひとつにリトライ機能があります。
途中でダウンロードに失敗しても、自動で途中からダウンロードを再開するため、いつの間にかダウンロードが失敗していて残念な気持ちになることを防げます。

Linux系OSには標準で入っているか、簡単に入れられます。
Windowsでも、CygwinやWSLで入れることができます。

## 時間をおく
ダウンロードが失敗する原因として、回線が込み合っている可能性があります。
特に、夜間は自宅に帰宅してインターネットを使う人が多く、回線が混雑しやすいです。
回線速度が遅いと感じる場合は、日中に再挑戦してみてはいかがでしょうか。
