---
title: "「Netlify DNS」に変えたら速くなった"
date: 2019-02-23T17:29:30+09:00
lastmod: 2020-02-08T18:32:00+09:00
author: "ぶっち"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1580351955/Blog-personal/thumbnail/blog.jpg"]
categories: ["プログラミング"]
tags: ["ブログ"]
archives: ["2019", "2019-02"]
toc: true
draft: false
---

*2020/02/08 追記*  
現在は Firebase Hosting でホスティングし、CloudFlareのDNSを使用しています。

このブログのDNSを、国内のドメイン管理会社から「Netlify DNS」に変更しました。
その結果、思ったよりDNS周りの処理が速くなったので、速度比較をしようと思います。

DNSの説明は、検索すれば見つかるのでそちらを参照してください。

## 前提
以下の状況でDNSを「Netlify DNS」に変えました。

* サブドメインは「www」
* 他社のDNSから「Netlify DNS」への移行

## やったこと
やったことは、ほとんど[こちらのサイトで紹介されている手順](https://www.techbuffet.net/2018/06/netlify-muumuudomain/ "ムームードメインで取得した独自ドメインをNetlifyに設定 - tech buffet")と同じです。

ドメインの管理パネルでネームサーバの変更をしないとDNSが切り替わらないので、気をつけてください。
Netlify側の操作では、表示されるメッセージを確認して、大丈夫そうならボタンを次々に押していけば、最低限きちんとした状態に設定されます。
とてもお手軽です！

Netlifyで管理している同じルートドメインの他のサイトも設定したい場合は、そのサイトのドメイン設定からNetlify DNSの設定をすれば、Netlify DNSにそのドメインについての項目を追加できます。
これも簡単です。
必要に応じて、IPv6のアクティベートをしても良いかもしれません（しなくても問題なし）。

## 比較
[Pingdom Tools](https://tools.pingdom.com/ "Pingdom Website Speed Test")というWebサービスを用いて、DNSの変更前後の通信の様子を観察しました。
このサービスは、どの国からアクセスするのかを設定できるので便利です。
日本も選べます。

これから通信の様子を比較しますが、**アクセスするタイミングによって大きく変わる**ものです。
参考程度にご覧ください。

### 移行前
以下の画像は移行前の通信の様子です。  
DNSはピンク色の帯で表されていますが、ピンク色の帯が全体に対して相対的に長いです。
どのサーバにアクセスすればいいのかを探しているという、まだWebページにアクセスしてさえいないのに、これほど時間がかかるのはもったいないです。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580349964/Blog-personal/netlify_dns/before.png"  alt="移行前" caption="移行前" >}}

### 移行後
以下の画像は移行後の通信の様子です。  
ピンク色の帯が一気に短くなりました。
DNS関連の処理にかかる時間が短くなっています。
反対に、黄色の帯で表されている、サーバからのデータの受け取りを待機する時間がとても長くなっています。
なぜでしょうね？
おそらくアクセスするタイミングによるのだと思います。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580349964/Blog-personal/netlify_dns/after.png"  alt="移行後" caption="移行後" >}}

### 比較
以下の表はDNSの移行前後の比較です。  
繰り返しになりますが、これは1回のみの測定結果です。
**アクセスするタイミングによって大きく異なること**にご注意ください。

この表を見ると、移行によってDNS関連の処理は短時間で終わるようになったことがわかります。
また、データのダウンロードも速くなっています。
反対に、データを受け取るまでの待ち時間がとても長くなっています。
その結果、処理全体としては時間があまり変わりません。

なんだか納得のいかない結果ですね。  
「Netlify DNS」に移行したことでDNSの処理が速くなった、ということで良しとしましょう。

|         |  移行前[ms]  |  移行後[ms]  |
| :----:  | ----:   | ----:   |
| *DNS*   |  160.3  |   13.6  |
| SSL     |   73.3  |   72.8  |
| Connect |  141.2  |  140.6  |
| Send    |    0.1  |    0.2  |
| *Wait*  |   69.8  |  304.0  |
| *Receive* |   64.2  |    1.3  |
| Blocked |    0.0  |    0.0  |
| *Total* |  509.0  |  532.5  |

## まとめ
「Netlify DNS」に移行してみて、DNS関連の処理は明らかに速くなりました！

国内のドメイン管理会社さんは、DNSは契約者の多くが使うと思いますし、もう少し頑張って欲しいですね。
むしろ、NetlifyのDNSの方が速すぎるのかもしれません。

以上から、もし「Netlify DNS」に移行可能でしたら、移行してみるとWebサイトの読み込みが
速くなるかもしれません。

## 番外編 ~Netlify ADN~
速度関連の話題として、ついでにNetlify ADNにも触れたいと思います。

ADNとは、Application Delivery Network の略称で、CDNみたいなものです。
Netlifyがいろいろ工夫しているので、Webサイトの配信が速くなるそうです。

このブログもADN上にあるので、きっと速いはずです。  
Netlifyが提供している[Testmysite.io](https://testmysite.io/ "Testmysite.io | Netlify Speedtest")というWebツールで、速度を計測してみます。

以下の画像は、世界中からこのブログにアクセスしたときの、データがブラウザに届き始めるまでの時間と、HTMLファイルを読み込み終わるまでの時間です。  
日本だけ長いですね。
それでも、70msというのは短い方だと思います。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580349964/Blog-personal/netlify_dns/testmysite.png"  alt="このブログのTestmysite.ioでの結果" caption="このブログのTestmysite.ioでの結果" >}}

また、[aguse](https://www.aguse.jp/ "aguse.jp: ウェブ調査")というWebサイトについての様々な情報を得られるWebツールで、このブログを調べてみました。
その結果、このブログのサーバの所在地はアメリカだったり、時にはギリシャだったりと、国内ではありませんでした。

おそらくサーバの所在地が、アメリカやブラジルといった国より日本の方が遠い位置にあるのでしょう。
これは意外な結果でした。

[こちらのサイト](https://katabame.hateblo.jp/entry/2018/12/05/031527 "静的サイトとTTFBの話 - katabame’s blog")によると、どうやら日本のノード（サーバ）がなくなってしまったようです。
確かに、日本にノードがあるなら、日本からのアクセスは日本のノードで返すでしょうしね。
[公式サイト](https://www.netlify.com/features/adn/ "Netlify Application Delivery Network | Netlify")の上部のアニメーションでは、日本にも点があるのに...
