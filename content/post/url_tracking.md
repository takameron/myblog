---
title: "どのページにアクセスしたか捕捉する方法 by Google検索"
date: 2022-02-04T08:27:00+09:00
lastmod: 2022-02-04T08:27:00+09:00
author: "たかめろん"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1638366401/Blog-personal/url_tracking/thumbnail.png"]
categories: ["Tips"]
tags: ["プライバシー"]
archives: ["2022","2022-02"]
toc: false
draft: false
---

Googleの検索結果は、たまに「このページに 4 回アクセスしています。前回のアクセス: 21/11/10」のように表示されることがあります。

検索結果のリンクをクリックしただけなのに、いったいどうやってカウントしているのか気になり、検索結果を触って気づいたことを書いておきます。

まず、単にリンクにカーソルを合わせると、ステータスバーには通常のURLが表示されます。

リンクをクリックしたまま少しカーソルを動かしてみると、URLがGoogleのものに変わりました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638366415/Blog-personal/url_tracking/1.png" alt="Googleの検索結果（URLがGoogleのものになっている）" caption="検索結果のURLがGoogleのドメインになっている" >}}

つまり、クリックした瞬間にURLをGoogleのものに差し替え、Googleの用意したページから本来のページへリダイレクトしているということです。

JavaScriptで捕捉しているだろうと思っていましたが、このような手法もあるのですね。
