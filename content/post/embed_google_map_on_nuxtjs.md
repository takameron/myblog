---
title: "Nuxt.jsにGoogle マップを貼り付ける"
date: 2020-07-27T15:41:06+09:00
lastmod: 2020-07-27T15:41:06+09:00
author: "ぶっち"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1594003909/Blog-personal/embed_google_map_on_nuxtjs/before.png"]
categories: ["プログラミング"]
tags: []
archives: ["2020", "2020-07"]
toc: false
draft: false
---

今年1月頃にハマった事例ですが、下書き記事を発掘したので、今さらながら加筆修正して紹介しようと思います。
[「Yahoo! JavaScriptマップAPI」にハマった](/post/cantviewyahoomap/) のと同時期の出来事です。

---

Nuxt.jsにGoogle マップを埋め込むとき、ただiframeのコードを貼り付けただけでは期待したように表示されません。

以下が「共有」→「地図を埋め込む」から取得したコードです。

```html {linenos=false}
<iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3240.6678649006717!2d139.7506108155666!3d35.68517933736224!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x60188c0d02d8064d%3A0xd11a5f0b379e6db7!2z55qH5bGF!5e0!3m2!1sja!2sjp!4v1580219879420!5m2!1sja!2sjp" width="600" height="450" frameborder="0" style="border:0;" allowfullscreen=""></iframe>
```

マップがとても小さくなってしまいます。
さらに、ドラッグしても動きません。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1594003909/Blog-personal/embed_google_map_on_nuxtjs/before.png"  alt="埋め込み用コードを貼り付けただけの地図表示" caption="変更前" >}}

取得したコードに、次の修正をします。

* 閉じタグを除去
* allowfullscreenを除去
* styleに`height`を設定

すると以下のコードになります。

```html {linenos=false}
<iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3240.6678649006717!2d139.7506108155666!3d35.68517933736224!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x60188c0d02d8064d%3A0xd11a5f0b379e6db7!2z55qH5bGF!5e0!3m2!1sja!2sjp!4v1580219879420!5m2!1sja!2sjp" width="600" height="450" frameborder="0" style="border:0; height:450px" />
```

大きく表示されるようになり、ドラッグにも反応するようになりました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1594003925/Blog-personal/embed_google_map_on_nuxtjs/after.png"  alt="コード修正後の地図表示" caption="変更後" >}}
