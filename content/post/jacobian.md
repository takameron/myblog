---
title: "ヤコビアンの求め方"
date: 2019-03-03T14:40:00+09:00
lastmod: 2019-03-03T14:40:00+09:00
author: "たかめろん"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1580351951/Blog-personal/thumbnail/study.jpg"]
categories: ["Tips"]
tags: ["勉強"]
archives: ["2019", "2019-03"]
toc: true
draft: false
---

ヤコビアンをなかなか理解できなかったので、備忘録として書き残します[^1]。

しっかりと理解しているわけではないので、間違いや補足すべき事項があるかもしれません。ご了承ください。

## 求め方
ヤコビアンは以下のように求めます。
{{< math inline >}}x{{< /math >}} , {{< math inline >}}y{{< /math >}} と {{< math inline >}}u{{< /math >}} , {{< math inline >}}v{{< /math >}} が反対でも転置行列となるため、行列式は変わりません。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1630398718/Blog-personal/jacobian/jacobian_uv.svg" w=580 h=332 caption="ヤコビアンの計算方法" >}}

変数 {{< math inline >}}x{{< /math >}} , {{< math inline >}}y{{< /math >}} を変数 {{< math inline >}}u{{< /math >}} , {{< math inline >}}v{{< /math >}} に変換したいとき、変換元の式は {{< math inline >}}x = {{< /math >}} や {{< math inline >}}y = {{< /math >}} の形になるように、式変形をします。

## 番外編１ ～極座標変換で出てくる r ～
極座標変換をすると、{{< math inline >}}dxdy{{< /math >}} は {{< math inline >}}r drd\theta{{< /math >}} で表されます。
この時のヤコビアン {{< math inline >}}r{{< /math >}} の導出方法を解説します。

最初に、{{< math inline >}}x{{< /math >}} と {{< math inline >}}y{{< /math >}} を極座標変換して、 {{< math inline >}}x = r \cos\theta{{< /math >}} , {{< math inline >}}y = r \sin\theta{{< /math >}} とおきます。

{{< math inline >}}x = r \cos\theta{{< /math >}} , {{< math inline >}}y = r \sin\theta{{< /math >}} について次のようにヤコビアンを計算すると、ヤコビアン {{< math inline >}}r{{< /math >}} が求まります。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1630398718/Blog-personal/jacobian/jacobian_r.svg" w=580 h=294 caption="rの導出方法" >}}

## 番外編２ ～(x-a)^2 + y^2 <= a^2～[[^2]]
{{< math inline >}}(x-a)^2 + y^2 \leqq a^2{{< /math >}} という式を極座標変換をしたときの、 {{< math inline >}}r{{< /math >}}の範囲について求めます。

1. 極座標変換した {{< math inline >}}x = r \cos\theta{{< /math >}}, {{< math inline >}}y = r \sin\theta{{< /math >}} を与式に代入
{{< math >}}(r\cos\theta -a)^2 + (r\sin\theta)^2 \leqq a^2{{< /math >}}
1. 展開
{{< math >}}r^2 \cos^2\theta - 2ar\cos\theta + a^2 + r^2\sin^2\theta \leqq a^2{{< /math >}}
1. {{< math inline >}}a^2{{< /math >}} を削除
{{< math >}}r^2 \cos^2\theta - 2ar\cos\theta + r^2\sin^2\theta \leqq 0{{< /math >}}
1. 「{{< math inline >}}\cos^2\theta + \sin^2\theta = 1{{< /math >}}」を使うためにまとめる
{{< math >}}r^2 ( \cos^2\theta + \sin^2\theta ) - 2ar\cos\theta \leqq 0{{< /math >}}
1. 「{{< math inline >}}\cos^2\theta + \sin^2\theta = 1{{< /math >}}」を適用
{{< math >}}r^2 - 2ar\cos\theta \leqq 0{{< /math >}}
1. 両辺から {{< math inline >}}r{{< /math >}} を割る
{{< math >}}r - 2a\cos\theta \leqq 0{{< /math >}}
1. {{< math inline >}}-2a\cos\theta{{< /math >}} を移項
{{< math >}}r \leqq 2a\cos\theta{{< /math >}}

半径 {{< math inline >}}r{{< /math >}} は、{{< math inline >}}r \geqq 0{{< /math >}} を満たします。

以上より、
{{< math >}}0 \leqq r \leqq 2a\cos\theta{{< /math >}}


[^1]: 数式をMathJaxで表示するとAMP環境で読み込みが遅くなることがわかったので、部分的にsvg形式の画像で埋め込んでいます（[TeXclip](https://texclip.marutank.net/ "TeXclip")というサービスを利用）。
[^2]: 見出しに数式らしく表示すると表示が壊れてしまうようなので、そのまま記述しました。
