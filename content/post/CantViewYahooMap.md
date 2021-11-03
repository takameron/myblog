---
title: "YOLP（地図）の「Yahoo! JavaScriptマップAPI」が表示されずに背景がグレーになってしまったときの対処法"
date: 2020-02-08T16:59:00+09:00
lastmod: 2020-02-08T16:59:00+09:00
author: "ぶっち"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1581084597/Blog-personal/CantViewYahooMap/CantViewYahooMap.jpg"]
categories: ["プログラミング"]
tags: []
archives: ["2020", "2020-02"]
toc: true
draft: false
---

## 症状

Nuxt.jsでYOLP（地図）の「Yahoo! JavaScriptマップAPI」を使おうとすると、背景がグレーのまま、ロゴとコントロールしか表示されませんでした。

灰色のところをドラッグするとカーソルが手を握った形になり、地図の画像が読み込まれているようでした。

え、謎すぎる...

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1581084597/Blog-personal/CantViewYahooMap/CantViewYahooMap.jpg" img_w=979 img_h=819 w=500 form="landscape" alt="背景が灰色のYOLPのマップ" caption="背景が灰色のYOLPのマップ" >}}

## 解決

これは解決したときの歓喜のツイート

{{< twitter user="takameron_info" id="1223876688108384256" >}}

[こちらのサイト](http://mori-coding.blog.jp/archives/8063243.html "yahoo map（YOLP）でマップが描画されずにグレーになったときのCSS原因 : 森のコーディング")に解決法が紹介されています。  
なんと！
地図として読み込まれている画像の、CSSの設定が原因でした。

div要素のidを `map` にしたとき、以下のCSSをあてると無事に地図が表示されました。

```css
#yahoo_map img {
    max-width:none;
}
```

## まとめ

実は、この問題に取り組んでいるときに、試しにGoogle Mapsのiframeを表示させようとしました。
しかし今度は、地図は表示されるものの、ドラッグしても動かない...

ブラウザの開発ツールでいじくっていると、CSSのheight属性が定義されていました。試しにチェックを外してみると、無事に動作しました！

Yahoo!地図もGoogle マップも、ドラッグ操作に応じて地図の画像を読み込んで表示しています。
外部サービスの画像が表示されないときは、CSSを疑って、とくに大きさを定義している場合は注意したほうが良いと、勉強になりました。
