---
title: "ポートフォリオページのリニューアル"
date: 2024-01-07T17:37:13+09:00
lastmod: 2024-01-07T17:37:13+09:00
author: "たかめろん"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1704612498/Blog-personal/portfolio_renewal_2024/thumbnail.png"]
categories: ["プログラミング"]
tags: ["ポートフォリオ","HUGO"]
archives: ["2024","2024-01"]
description: "ポートフォリオを作り直しました。HUGOで新しくテーマを作成し、Bulmaを使ってデザインしました。"
toc: false
draft: false
---

[ポートフォリオ](https://portfolio.takameron.info/)を作り直しました。

ポートフォリオは[HUGO](https://gohugo.io/)という静的サイトジェネレータで作成しており、もともとはとても高機能なテーマを使っていました（[こちらのリポジトリ](https://github.com/takameron/portfolio)で管理しています）。
HUGOは更新が多く、新機能がどんどん追加され、それでもサクサクと動き本当に素晴らしいです。
それにあたって後方互換性のない変更も多く、テーマの対応が必要になるタイミングもたくさんあります。

もともとのポートフォリオも、HUGOのバージョンを上げるとサイトをビルドできなくなりました。
テーマはメジャーバージョンアップしたものが出ていましたが、テーマが高機能なのもありバージョンアップの仕方がわかりませんでした。
静的サイトジェネレータは古いものを使っていてもセキュリティの問題などはないと思いますが、私は常に最新を使いたい！！（笑）

そこで、私の私による私のためのポートフォリオ用テーマを自作しよう！ということで一から作りました。
このブログサイトも[自作テーマ](https://github.com/takameron/hugo_theme_smartblog)を使っていますが結構手が込んでいるので、ポートフォリオはできるだけシンプルに、shortcodeは作らず、デザインはCSSを書かずにBulmaで済ませました。

できた自作テーマは[こちら](https://github.com/takameron/hugo_theme_portfolio)です。

そして、ポートフォリオを管理するリポジトリは[こちら](https://github.com/takameron/myportfolio)です。

HUGOの[Data templates](https://gohugo.io/templates/data-templates/)という機能がとても便利で、各種リンクやスキル、取得した資格・試験を書くときに、YAML,JSON,XML,TOML形式のファイルで管理できます。
追加や削除が簡単で分かりやすいのが良いですね。

そして初めてBulmaですべてのデザインをしましたが、わりと簡単にモダンな見た目にできて最高でした。
個人的にJavaScriptを減らしたいという気持ちがあったので、ピュアCSSなのも好みです。

CSSではいろいろなプロパティを指定しますが、Bulmaでは機能や役割にあったクラスを指定すると良さげな見た目になるので、CSSへの理解が浅くても気軽にデザインを当てられるのが良いと思いました。
また、目的に対して、それを実現する方法が基本的に一つだけなのも、迷うポイントが少なくていいなと思いました。
CSSは古いプロパティ、新しいプロパティ、ブラウザの対応状況など考慮することがいろいろあり、さらにやりたいことに対して方法が複数あるのが悩みやすいポイントかなと思います。

ようやくポートフォリオを作り直しました！
これでポートフォリオを更新しやすくなったと思いますし、常に最新を使えるという満足感もあります。
PageSpeed Insightsの結果があまり良くないのは気になりますが、一人がたくさん使うようなサイトではないですし、体感では十分に速いので気にしないことにします😅

楽しく、良い経験になりました。

---

雑記

ポートフォリオサイトはCloudflare Pagesで管理していますが、portfolio.takameron.infoという同じドメインに対してGitHubのリポジトリを変える機能は存在せず、いったん旧サイトからCustom Domainを外し、新サイトにCustom Domainを付与する必要がありました。

やってみたところ、旧サイトからCustom Domainを外すとすぐにサイトにアクセスできなくなりましたが、新サイトにCustom Domainを付与してからアクセスできるようになるまでに1時間半ほどかかりました。

CNAMEレコードが変わっているだけなので、DNSの浸透待ちが原因であれば、Custom Domainを外した直後にアクセスできなくなったのならCustom Domainを付与した直後にアクセスできるようになっても良さそうに思うのですが、そういうわけではないのでしょうか🤔

不思議だなーと思ったので書き残しておきます。
