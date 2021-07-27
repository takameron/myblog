---
title: "Web版「pixiv Sketch」でペンタブが使えないときの対処法"
date: 2020-04-12T10:41:30+09:00
lastmod: 2020-04-12T10:41:30+09:00
author: "ぶっち"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1584257891/Blog-personal/thumbnail/illust.jpg"]
categories: ["ソフトウェア・サービス"]
tags: []
archives: ["2020", "2020-04"]
toc: true
draft: false
---

pixivが提供している『[sensei](https://sensei.pixiv.net/ "イラストの描き方を動画で学ぶ！ - sensei by pixiv")』というサービス（イラストの描き方を動画で学べる）で、お題をやろうにも上手に（技術的に）描けませんでした。
その解決法を書き残しておきます。

## 環境

- Firefox 72.0.2 (64 ビット)
- Wacom Intuos Small ワイヤレス

## 問題

- ペンタブで絵が描けない
- 線が薄い・塗りつぶしで全面が塗り潰されてしまう

## 解決法

解決法を紹介します！
案外簡単な原因なんですけどね(^_^;)

### ペンタブで絵が描けない

ヘルプの[ドロー機能で筆圧を利用するにはどうすればよいですか？](https://sketch.pixiv.help/hc/ja/articles/115003339574-ドロー機能で筆圧を利用するにはどうすればよいですか- "ドロー機能で筆圧を利用するにはどうすればよいですか？ - pixiv Sketch よくある質問")を確認すると、以下のようになっています。

> 筆圧に対応しているブラウザは下記の通りです。
> * Windows
>   * Microsoft Edge
>   * Internet Explorer 11
>   * Google Chrome v59以降
> * Mac
>   * Google Chrome
>
> ワコム製品をお使いの方は、タブレットのプロパティからオプションの「デジタルインク機能をつかう」をオンにしてください。

おっと、FireFoxでは対応していないんですね(・_・;)

Google Chromeを使ってみると、無事にペンタブで絵を描けました！

### 線が薄い・塗りつぶしで全面が塗り潰されてしまう

下の画像のように、目玉焼きみたいな丸の線が薄いですよね...
絵を描いていると、もっと線が濃くならないかな、と思います。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584256967/Blog-personal/cannot_use_pen_tab_on_pixiv_Sketch_web/pixiv_Sketch_thin1.png"  alt="薄い線で3重に描いた丸" caption="薄い線で描いた丸" >}}

問題なのが、これ。塗りつぶしをしたときに、線の囲いを突破してしまうこと。
髪の毛をとりあえず塗りつぶそうとしたら、まさか全体が塗りつぶされて驚きました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584256967/Blog-personal/cannot_use_pen_tab_on_pixiv_Sketch_web/pixiv_Sketch_thin2.png"  alt="一部の除いて意図しないところまで塗りつぶされてしまった" caption="塗りつぶしが線をはみ出している" >}}

なんと筆記具の種類を変えることができます！
ここでペンのようなものに変えると、色は濃くなり、塗りつぶしもできるようになりました。上の画像では、ペンで囲ったところは塗りつぶしから除外されています。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584256967/Blog-personal/cannot_use_pen_tab_on_pixiv_Sketch_web/pixiv_Sketch_thin3.png" img_w=405 img_h=633 w=405 form="landscape" alt="数種類のペン" caption="筆記具を選べる" >}}

## まとめ

困ったときは[よくある質問](https://sketch.pixiv.help/hc/ja "pixiv Sketch よくある質問")を読みましょう！
