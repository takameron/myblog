---
title: "Google Analyticsにカウントされない方法"
date: 2019-03-07T15:03:00+09:00
lastmod: 2020-05-12T06:00:23+09:00
author: "ぶっち"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1580351955/Blog-personal/thumbnail/blog.jpg"]
categories: ["Tips"]
tags: ["ブログ"]
archives: ["2019", "2019-03"]
toc: true
draft: false
---

Google Analyticsを設置しているWebサイトに、自分のアクセスをカウントされないようにする方法を紹介します。

Google Analyticsを回避する方法は、検索すればたくさんの情報が出てきます。  
ここでは、私が行っている方法について紹介します。

## 「Google アナリティクス オプトアウト アドオン」
まずは、「Google アナリティクス オプトアウト アドオン」というアドインを利用することです。
これはGoogleが提供している、公式のアドインです。
このアドインをブラウザにインストールすると、そのブラウザでアクセスした時に、自分のアクセスがカウントされなくなります。

ちなみに、私は利用していません。
検索すれば紹介記事はたくさんあるので、ここでは簡単な紹介にとどめます。

このアドインは、以下のリンクから導入することができます。  
{{< blogcard "https://tools.google.com/dlpage/gaoptout?hl=ja" >}}

### 利点
簡単に利点をあげると、以下の点が利点だと思います。

* 多くのブラウザに対応している
* 導入が簡単

2019/03/05時点で、ダウンロードページによると Microsoft Internet Explorer 11、Google Chrome、Mozilla Firefox、Apple Safari、Opera に対応しているそうです。
意外と幅広く対応していますね。

また、アドインをインストールするだけなので、導入も簡単です。

### 欠点
欠点は、以下の点が挙げられます。

* すべてのWebサイトでカウントされなくなる

自分が所有するWebサイトへの自分のアクセスを除外したい場合、他のすべてのサイトも巻き込んでしまうのは申し訳なさがあります。
自分も正確なアクセス数を把握したいからGoogle Analyticsを設置して自分のアクセスを除外しようとしているので、他の方々にも正確なアクセス数を提供した方が良いかと思います。

もちろん、あらゆるサイトに自分のアクセスを把握されたくない、という場合でしたら、このアドインをブラウザごとに導入することで目的は果たせます。
ただし、このアドインはGoogle Analyticsにデータを送信しないだけで、他のアクセス解析サービスには解析されることに注意してください。

## Firefoxの「プライベートブラウジング」
Firefoxの「プライベートブラウジング」を利用すると、コンテンツブロッキング機能がアクセス解析といったトラッカーをブロックします。
これによって、Google Analyticsに情報が送信されません。

### 使い方
Firefoxには、デスクトップ版とモバイル版があります。

#### デスクトップ版
デスクトップ版では、プライベートウィンドウを開いて、目的のWebサイトにアクセスします。

自分のWebサイトなどをブックマークに保存しておけば、簡単に目的のWebサイトを閲覧することができます。

以下のリンクから、Firefoxをダウンロードできます。  
{{< blogcard "https://www.mozilla.org/ja/firefox/" >}}

#### モバイル版
スマートフォン用のFirefoxには、プライバシー保護を重視した『Firefox Focus』というアプリがあります。
AndroidとiOSに対応しています。

このアプリでWebサイトを閲覧すると、デスクトップ版のプライベートウィンドウのような機能を果たします。
すなわち、トラッカーは無効化し、キャッシュはブラウザの終了後に削除されます。

このアプリの欠点は、ブックマークという機能がないことです。
そのため、よく見るWebサイトはホーム画面にアイコンを作ると便利です。

以下のリンクから、Androidのダウンロードページに移動します。  
{{< blogcard "https://play.google.com/store/apps/details?id=org.mozilla.focus" >}}

### 利点
Firefoxの利点は、以下の点が挙げられます。

* 任意のWebサイトだけ、カウントされない
* さまざまな環境で利用できる

目的のWebサイトを閲覧したい時だけブラウザを切り替えることで、任意のWebサイトだけにトラッキングされなくなります。

普段は、使い慣れているブラウザで普通にWebサイトを閲覧することができます。
普段のWebサイトの閲覧に影響を及ぼしません。

また、FirefoxはWindows, Mac, Linux, Android, iOSといった、たくさんのOSに対応しています。
ほとんどの環境で使用可能です。

### 欠点
反対に、欠点は以下の点が挙げられます。

* ブラウザのインストールが必要
* 面倒くさい

もともとFirefoxを使用していなければ、Firefoxをインストールしなければいけません。
これは、アドインをインストールするよりも面倒です。

また、目的のWebサイトを開くときだけブラウザを切り替えるのも、面倒です。

## Brave
**2020/05/12 追記**  
Braveという、プライバシーと速度を重視したブラウザーがあります。
Google Chromeをベースにプライバシー機能や仮想通貨ウォレットなどを追加したブラウザです。広告やトラッキングコードをブロックする機能があるため、Google Analyticsの読み込みもブロックされます。

ユーザにとっては余計なものの読み込みをブロックするため、比較的高速なブラウザです。
また、Google Chromeの拡張機能もそのまま使えます。
ブラウザとしても優秀なので使ってみてはいかがでしょうか。

{{< blogcard "https://brave.com/ja/" >}}

## まとめ
理想的には、使い慣れているブラウザでボタン一つでトラッキングを防ぐか否かを切り替えられればいいですね。
または、URLを登録しておくと、そのURLの時だけはトラッキングを防止する、という機能があると、便利かもしれません。

検索すれば、今回挙げた方法以外にも見つかります。  
必要に応じて検索してみてください。

## 番外編～IPアドレスでの除外～
ちなみに、Google Analyticsには指定したIPアドレスからのアクセスを除外する機能があります。

しかし、それはIPアドレスが固定である企業などが使用する機能です。
個人では、そもそも接続場所によってIPアドレスが変わります。
例えば、自宅からのアクセスと外出先でのアクセスでは、IPアドレスが異なります。
また、自宅のIPアドレスも変わります。

そのため、IPアドレスを指定しただけでは、自分のアクセスを完全に除外することはできません。