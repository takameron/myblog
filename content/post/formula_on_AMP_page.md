---
title: "AMPに対応したHUGOサイトに数式を載せる"
date: 2019-02-27T15:20:00+09:00
lastmod: 2022-03-17T16:13:00+09:00
author: "たかめろん"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1580351955/Blog-personal/thumbnail/blog.jpg"]
categories: ["プログラミング"]
tags: ["ブログ","HUGO"]
archives: ["2019", "2019-02"]
toc: true
draft: false
---

HUGOで構築され、AMPに対応したWebサイトで、エラーなく数式を表示する方法を紹介します。

## **2022年3月17日追記**  
2022年現在ではGoogle検索におけるAMPの優位性はなく、AMPページに数式を載せようと四苦八苦するくらいならAMPに対応しない、という選択もあると思います。
画像のサイズを明記するなど、AMPで必須とされているものは確かに高速化につながっていると思います。
しかし全て完璧にしなければならず、そのための対応コストは大きいです。

ここでは簡単に、2022年版の数式の載せ方を紹介します。

まず、Shortcodesを作成します。  
以下の内容で、通常用の`math.html`、AMPページ用の`math.amp.html`を作成してください。

`math.html`
```plain {linenos=false}
{{- if .Get 0 -}}
\( {{ .Inner }} \)
{{- else -}}
\[ {{ .Inner }} \]
{{- end -}}
```

`math.amp.html`
```plain {linenos=false}
<amp-mathml layout="container" {{ if .Get 0 }} inline {{ end }} data-formula="\( {{ .Inner }} \)"></amp-mathml>
```

次に、数式表示用のライブラリを読み込みます。
`.HasShortcode "math"`は、`math`というShortcodesが使われていれば真、使われいなければ偽を返します。
これで数式が使われいるときだけライブラリを読み込めるようになります。

以下では、`math`というShortcodesが使われているときだけKaTeXというライブラリを読み込むコードの例です。

```html
{{- if .HasShortcode "math" -}}
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.15.3/dist/katex.min.css" integrity="sha384-KiWOvVjnN8qwAZbuQyWDIbfCLFhLXNETzBQjA/92pIowpC0d2O3nppDGQVgwd2nB" crossorigin="anonymous" media="print" onload="this.media='all'; this.onload=null;">
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.15.3/dist/katex.min.js" integrity="sha384-0fdwu/T/EQMsQlrHCCHoH10pkPLlKA1jL5dFyUOvB3lfeT2540/2g6YgSi2BL14p" crossorigin="anonymous"></script>
<script defer src="https://cdn.jsdelivr.net/npm/katex@0.15.3/dist/contrib/auto-render.min.js" integrity="sha384-+XBljXPPiv+OzfbB3cVmLHf4hdUFHlWNZN5spNQ7rmHTXpd7WvJum6fIACpNNfIR" crossorigin="anonymous"></script>
<script>
  document.addEventListener("DOMContentLoaded", function() {
    renderMathInElement(document.body, {
      delimiters: [
        {left: "$$", right: "$$", display: true},
        {left: "$", right: "$", display: false},
        {left: "\\(", right: "\\)", display: false},
        {left: "\\[", right: "\\]", display: true}
      ]
    });
  });
</script>
{{- end -}}
```

Shortcodesの使い方を紹介します。

1行全体を使って数式を表示するには、以下のようにします。
```plain {linenos=false}
{{</* math */>}} x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a} {{</* /math */>}}
```

文中（インライン）に表示するには、以下のように`inline`を書き加えます。
```plain {linenos=false}
{{</* math inline */>}} x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a} {{</* /math */>}}
```

---

## 概要
ここでは、大まかな流れを説明します。
実際の方法を見たい方は[次の章](#ライブラリの読み込み)からご覧ください。

通常のページとAMPのページではさまざまな差があり、AMPの方が制約が厳しいです。
AMPでは、ごく限られた一部のJavaScriptしか使えないというのが、大きな問題になります。

以下が構築の流れです。

1. 通常ページとAMPページでテンプレートを分け、それぞれライブラリを読み込む
1. 通常ページとAMPページごとにShortcodesを作成
1. 数式を表示したい記事のフロントマターの設定
1. Shortcodesを用いて数式の表示

### 通常ページとAMPページ {#ordinary_vs_amp}
通常ページとAMPページでは、異なる対応をします。
これは、AMPでは一部のJavaScriptしか使えず、広く使われている数式表示ライブラリを使えないからです。

### フロントマターによってライブラリの読み込みを判断
フロントマターとは、記事ファイル上部にある各種設定が書かれている部分のことです。

フロントマターに`Math`パラメータを設定し、この値に応じて、ライブラリを読み込むか否かを判断します。
これは、数式が使われてない記事を表示するときに、数式表示ライブラリを読み込むのを防ぐためです。
AMPの仕様では、不要なコンポーネントを読み込むとエラーになります。
使用しないのに数式表示ライブラリを読み込むとエラーとなるため、このような対応をします。

### Shortcodesの使用
Shortcodesとは、部品のようなものです。
必要に応じて値を渡すことができ、記事中でShortcodesを置いたところにShortcodesの処理結果が埋め込まれます。

通常ページとAMPページで用いるライブラリが違うと、インライン表示（文に混ぜる）と単独表示（？）の指定などが異なります。
そのため、記事中のShortcodesで数式とともに表示方法の指定をすれば、Shortcodes側で処理をするようにします。

この記事では、このブログで使用している[Robust](https://github.com/dim0627/hugo_theme_robust "GitHub - dim0627/hugo_theme_robust" )というテーマに沿って説明します。

## ライブラリの読み込み
通常ページとAMPページでは、使用するライブラリ（コンポーネント）が異なります。

### 通常ページ
通常ページでは、Webサイトで数式を表示するために広く使われている、MathJax を使用します。

まず、`themes\hugo_theme_robust\layouts\_default\baseof.html`を`layouts\_default\baseof.html`にコピーします。
このファイルは、Webページの土台のようなものです。

次に、コピーした`baseof.html`ファイルのヘッダー（`<head>`～`</head>`で囲まれている部分）のどこかに、以下のコードを貼り付けます。

```html
{{ if .Params.Math }}
<script async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.3/MathJax.js?config=TeX-AMS_CHTML"></script>
{{ end }}
```

### AMPページ {#library-amp}
AMPページでは、MathJaxなどのJavaScriptを使用できません。
その代わりに、「[amp-mathml](https://www.ampproject.org/docs/reference/components/amp-mathml "amp-mathml – AMP")」という数式を表示するためのコンポーネントが提供されています。

まず、`themes\hugo_theme_robust\layouts\_default\baseof.amp.html`を`layouts\_default\baseof.amp.html`にコピーします。
このファイルは、AMPページにおいて`baseof.html`の代わりになるものです。

次に、コピーした`baseof.amp.html`ファイルのヘッダーのどこかに、以下のコードを貼り付けます。

```html
{{ if .Params.Math }}
<script async custom-element="amp-mathml" src="https://cdn.ampproject.org/v0/amp-mathml-0.1.js"></script>
{{ end }}
```

## Shortcodesの作成

### 通常ページ
`layouts\shortcodes\math.html`というファイルを作成し、以下のコードを貼り付けます。

```html
{{ if .Get "inline"}} \( {{ .Get "formula" }} \) {{ else }} \[ {{ .Get "formula" }} \] {{ end }}
```

### AMPページ {#shortcodes-amp}
`layouts\shortcodes\math.amp.html`というファイルを作成し、以下のコードを貼り付けます。

```html
<amp-mathml layout="container" {{ if .Get "inline"}} inline {{ end }} data-formula="\( {{ .Get "formula" }} \)"></amp-mathml>
```

## フロントマターの設定
フロントマターのどこかに、数式を表示したい記事では`math: true`という記述を加えます。
数式を表示しない記事では`math: false`という記述を加えるか、何も記述をしません。

必要に応じて`themes\hugo_theme_robust\archetypes\default.md`を`archetypes\default.md`にコピーし、フロントマターに`math: false`と加えておくと、簡単に数式を表示するか否かを切り替えられて便利だと思います。


以下が、数式を表示する記事のフロントマターの例です。
いろいろな書き方があるので、ご自身のフロントマターの書き方に合わせてください。
```YAML
---
draft: true
thumbnail: ""
tags: ["数学"]
date: "2019-02-25T00:30:00+09:00"
title: "いろいろな数式の紹介"
description: ""
toc: true
math: true
---

ほげほげ
```

## 数式の記述
Shortcodesを用いて数式を埋め込みます。

表示結果は、[この記事のAMP版](/amp/post/formula_on_amp_page/)でもご確認ください。

インライン表示にするか否かは、`inline`パラメータを読み取っています。
インライン表示にしたければ`inline="true"`、1行表示なら`inline=""`を指定します。
この辺は、もっと良い方法があるかもしれません。

### インライン表示
インライン表示の場合は、記事中に例えば次のように書きます[^1]。

```html {linenos=false}
今回は、{{</* math formula="ax^2 + bx + c = 0" inline="true" */>}}という式について解説します。
```

すると、結果は次のようになります。

> 今回は、{{< math inline >}}ax^2 + bx + c = 0{{< /math >}}という式について解説します。

### 1行表示
数式を1行で表示する場合は、例えば次のように書きます。

```html {linenos=false}
次に、二次方程式の解の公式を示す。{{</* math formula="x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}" inline="" */>}}
```

すると、結果は次のようになります。

> 次に、二次方程式の解の公式を示す。{{< math >}}x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}{{< /math >}}

これで、記事中に数式を表示できるようになりました。


[^1]: この部分は、`{{</*/* math formula="ax^2 + bx + c = 0" inline="true" */*/>}}`のように書いて、エスケープしました。
