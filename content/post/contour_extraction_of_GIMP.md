---
title: "GIMPで輪郭抽出"
date: 2020-03-01T17:38:30+09:00
lastmod: 2020-03-01T17:38:30+09:00
author: "たかめろん"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1583049405/Blog-personal/contour_extraction_of_GIMP/processed.jpg"]
categories: ["ソフトウェア・サービス"]
tags: []
archives: ["2020", "2020-03"]
toc: true
draft: false
---

みんなで写真を撮った後、顔をぼかしてからSNSにあげると味気ないですよね。  
輪郭を抽出すると、人の特徴をぼやかしながら、おもしろい写真ができます！

たとえば、以下のように。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1583049405/Blog-personal/contour_extraction_of_GIMP/origin.jpg"  alt="元画像" caption="元画像" >}}

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1583049405/Blog-personal/contour_extraction_of_GIMP/processed.jpg"  alt="輪郭抽出後" caption="輪郭抽出後" >}}

本当はヒトの顔を題材にしたかったのですが、肖像権もありますし、可愛いペンギンにモデルになってもらいます！（笑）

## GIMPのインストール
GIMPとは、無料で使える商用レベルの画像編集・加工ソフトウェアです。
まだインストールしていない方は、[公式サイト](https://www.gimp.org/ "GIMP - GNU Image Manipulation Program")からダウンロードして、インストールしてください。

### コラム
GIMPという名称は「GNU Image Manipulation Program」の略です。しかし、「GIMP」という差別用語もあるそうです。そのため、TwitterでGIMPという単語を入れると、アカウントを凍結される恐れがあるそうです。気をつけてください。

## 起動
最初に、GIMPで加工したい画像を開きます。
開く方法はなんでもいいですが、たとえば以下の方法があります。

- エクスプローラーで画像ファイルを右クリックし、コンテキストメニュー内の「プログラムから開く」から起動
- GIMPを起動し、画像ファイルをドラッグ＆ドロップでGIMPのウィンドウに入れる
- GIMPを起動し、GIMPのファイルメニューから起動

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1583049405/Blog-personal/contour_extraction_of_GIMP/1.jpg"  alt="GIMPで画像を開く" caption="GIMPで画像を開く" >}}

## 輪郭抽出
GIMPには、なんと輪郭抽出をする機能があります！高度なアルゴリズムを使った画像処理が簡単にできて便利です。

1. 「フィルター」→「輪郭抽出」→「輪郭」をクリック

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1583049405/Blog-personal/contour_extraction_of_GIMP/2.jpg"  alt="メニューから「輪郭」を選択" caption="メニューから「輪郭」を選択" >}}

2. 各種パラメータはお好みですが、今回はAlgorithmを「Sobel」にします

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1583049405/Blog-personal/contour_extraction_of_GIMP/3.jpg"  alt="「輪郭」フィルタのパラメータを選択" caption="パラメータを選択" >}}

これで、版画のようになりました。

## 色の反転

このままだと全体的に暗いので、色を反転させます。

1. 「色」→「階調の反転」をクリック

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1583049406/Blog-personal/contour_extraction_of_GIMP/4.jpg"  alt="メニューから「階調の反転」を選択" caption="メニューから「階調の反転」を選択" >}}

これで背景が白、線が黒になりました。

## 脱色
なんとなく、脱色の処理をします（笑）結果にあまり変化はありませんが、白黒で輪郭抽出するために、一応やっておきます。

1. 「色」→「脱色」→「Desaturate」をクリック

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1583049406/Blog-personal/contour_extraction_of_GIMP/5.jpg"  alt="メニューから「Desaturate」を選択" caption="メニューから「Desaturate」を選択" >}}

2. 各種パラメータはお好みですが、ここではそのままにしておきます

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1583049406/Blog-personal/contour_extraction_of_GIMP/6.jpg"  alt="「脱色」フィルタのパラメータを選択" caption="パラメータを選択" >}}

## 線をクッキリさせる
線がぼんやりしているときは、線をシャープにするフィルターをかけます。

1. 「フィルタ」→「強調」→「シャープ（アンシャープマスク）」をクリック

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1583049406/Blog-personal/contour_extraction_of_GIMP/7.jpg"  alt="メニューから「シャープ」を選択" caption="メニューから「シャープ」を選択" >}}

2. パラメータを調整するウィンドウが表示されます

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1583049406/Blog-personal/contour_extraction_of_GIMP/8.jpg"  alt="パラメータ調整ウィンドウ" caption="パラメータ調整ウィンドウ" >}}

3. 各種パラメータはお好みですが、今回は Radius:10, Amount:1, Threshold:0 にします

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1583049404/Blog-personal/contour_extraction_of_GIMP/9.jpg"  alt="「シャープ」フィルタのパラメータを選択" caption="パラメータを選択" >}}

線が濃くはっきりとしました。

これで、完成です！

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1583049405/Blog-personal/contour_extraction_of_GIMP/processed.jpg"  alt="輪郭抽出後" caption="輪郭抽出後" >}}

## 保存
保存は、2種類あります。

GIMPの内部形式で保存するには、「ファイル」→「保存」をクリックして保存します。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1583049404/Blog-personal/contour_extraction_of_GIMP/10.jpg"  alt="GIMPの内部形式で保存" caption="GIMPの内部形式で保存" >}}

PNG画像やJPEG画像として保存するには、「ファイル」→「Export As」をクリックして保存します。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1583049404/Blog-personal/contour_extraction_of_GIMP/11.jpg"  alt="PNGやJPEGなどで保存" caption="PNGやJPEGなどで保存" >}}

## まとめ
GIMPには、まだまだたくさんの機能があります！
いろいろな加工を試して、遊んでみてはいかがでしょうか。
