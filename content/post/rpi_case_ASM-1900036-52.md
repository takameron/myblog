---
title: "KSYのショップで購入した Raspberry Pi 3B＋・3・2・B＋ 用ケースの取付方法"
date: 2019-10-13T17:22:00+09:00
lastmod: 2019-10-13T17:22:00+09:00
author: "ぶっち"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1580350035/Blog-personal/rpi_case_ASM-1900036-52/thumbnail.jpg"]
categories: ["電子工作"]
tags: ["Raspberry Pi"]
archives: ["2019", "2019-10"]
toc: true
draft: false
---

先日、「Raspberry Pi Shop by KSY」にて Raspberry Pi 3B＋ のスターターキットを購入しました。
ちなみに最近はいろいろと遊べそうなものを購入しているので、いつかご紹介したいなぁ、と思っています。

ところが、スターターキットに含まれているケースが非常にはめづらく、私が不器用なのもあり2～3時間近く格闘する羽目になってしまいました。
格闘しているうちにコツを見つけたので、サクッとはめられるコツをメモしておきたいと思います。

## ケース紹介
今回は以下のケースを使用しました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580350035/Blog-personal/rpi_case_ASM-1900036-52/thumbnail.jpg"  alt="ASM-1900036-52" caption="ASM-1900036-52" >}}

日本の公式サイトでは、こちらで販売されています。

* [Raspberry Pi Shop by KSY](https://raspberry-pi.ksyic.com/main/index/pdp.id/427/pdp.open/427 "Piケース RS V3 赤 for 3B+/3/2/B+ [167-7053] | Raspberry Pi Shop by KSY")
* [RS Components](https://jp.rs-online.com/web/p/raspberry-pi-cases/1677053/ "ASM-1900036-52 | DesignSpark Raspberry Piケース, ABS樹脂 ASM-1900036-52 | RS Components")

ケースは、さすが公式で販売されているだけあって、使いやすくデザインも良いと感じます。
3つのパーツから構成されるため、慣れてしまえば取り付けやすいと思います。
また、ケースの蓋のパーツは取り付けても2mmほど浮いています。
さらに底面のパーツはメッシュ状になっているため、通気性がよく、熱対策がされています。

もちろんケースはRaspberry Piにピッタリですし、ラズベリーのマークが可愛いです！
さらに、ケース内にカメラモジュールを内包できるらしいです（未確認）。
カラーも4色展開（白・黒・赤・透明）で、複数のRaspberry Piを用途別に色分けできます。  
私は満足しています！

## 取り付け方
取り付けは、以下の手順で行うと上手にできます！  

1. 底面パーツにRaspberry Piをはめる
1. 本体パーツをはめる
1. 蓋パーツを取り付ける
1. microSDHCカードを挿入

はめるときに少し強めの力が必要になることがあります。
ただし、「どうしても、はめられない！」という時は、無理にはめようとすると、Raspberry Piかケースを破損する恐れがあります。
まずはパーツを外してから、再挑戦してみてください。

### 底面パーツにRaspberry Piをはめる
以下のように、底面パーツにRaspberry Piをはめます。  
Raspberry Piに合わせてケースが作られているので、ピンポイントではまるはずです。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580350035/Blog-personal/rpi_case_ASM-1900036-52/1.jpg"  >}}

{{< warning >}}
底面パーツに、飛び出している箇所があります。
この出っ張りの下にRaspberry Piを滑り込ませてください。
そうしないと後で綺麗にはまりません。
{{< /warning >}}

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580350035/Blog-personal/rpi_case_ASM-1900036-52/2.jpg" img_w=1400 img_h=1400 w=250 h=250 form="landscape" >}}

### 本体パーツをはめる
次に、本体パーツをはめます。  
向きは、Raspberry Piが本体パーツに、しっかりとはまりそうな向きにします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580350036/Blog-personal/rpi_case_ASM-1900036-52/3.jpg"  >}}

両方のパーツを裏返して、本体パーツを机に置き、Raspberry Piが取り付けられた底面パーツをはめると、成功しやすいです。
Raspberry Piは底面パーツの出っ張りで底面パーツに取り付けられているので、落下することはないはずです。

まずは、底面パーツの凹みがある方（microSDカード挿入口のある方）を下に押し込んで、本体パーツにはめます。
次にUSBやLANポートがある方を下に押し込んで、本体パーツに完全にはめます。

はめているときに、なかなかはまりそうでないときは、いったん底面パーツを本体パーツから外してから、再挑戦してください。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580350037/Blog-personal/rpi_case_ASM-1900036-52/4.jpg"  >}}

はめると、上から見た時に以下のようになります。  
ヒートシンクは、本体パーツの穴のあいている箇所にあるので、邪魔になることはありません。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580350036/Blog-personal/rpi_case_ASM-1900036-52/5.jpg"  >}}

### 蓋パーツを取り付ける
最後に、蓋パーツを取り付けます。  
取り付けた時に蓋が2mmほど浮きますが、それは正常です。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580350035/Blog-personal/rpi_case_ASM-1900036-52/6.jpg"  >}}

### 完成！
完成です！  
側面から見ると、以下のようになります。
ピッタリとRaspberry Piがケースにはまっていますね！

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580350036/Blog-personal/rpi_case_ASM-1900036-52/7.jpg"  >}}
{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580350036/Blog-personal/rpi_case_ASM-1900036-52/8.jpg"  >}}

### microSDHCカードを挿入
microSDHCカードの挿入方法です。  
底面パーツの凹みの部分に、microSDHCカードの挿入口があります。

以下のように、カードの表（図柄がある方）を手前にして、挿入してください。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580350037/Blog-personal/rpi_case_ASM-1900036-52/9.jpg"  >}}
{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580350037/Blog-personal/rpi_case_ASM-1900036-52/10.jpg"  >}}

カードを取り外すときは、Raspberry Pi 3の場合は、爪か何かで、なんとか引き抜いてください。
カードを押しても、飛び出してきません。
やや大変です。

## まとめ
2～3時間格闘した末につかんだコツをご紹介しました。
説明書も何もないので、何も知らずに試行錯誤するのは大変だなぁ、と感じます。

ケースもRaspberry Piも破損しないよう、上手にケースを取り付けてください！