---
title: "USBメモリに入れたUbuntuが起動しなくなったので修復した"
date: 2020-03-06T13:45:49+09:00
lastmod: 2020-03-06T13:45:49+09:00
author: "たかめろん"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1580351710/Blog-personal/Ubuntu_on_USB_does_not_start/not_booting.jpg"]
categories: ["Tips"]
tags: []
archives: ["2020", "2020-03"]
toc: true
draft: false
---

## USBメモリから起動しない
> Superblock checksum does not match superblock while trying to open /dev/sdb2

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580351710/Blog-personal/Ubuntu_on_USB_does_not_start/not_booting.jpg"  alt="起動エラー画面" caption="USBメモリから起動できなくなったUbuntu" >}}

というエラーメッセージが出て、USBメモリにインストールしていたUbuntuが起動できませんでした。

対処法が画面に書かれている通り、以下のコマンドでOKでした。

```plain {linenos=false}
e2fsck -b 8193 /dev/sdb2
```

エラーメッセージには2つのコマンドがあり、どちらにすればいいか迷った挙げ句、最初に `e2fsck -b 32768 /dev/sdb2` を実行してみましたが、エラーが出ました。
気を取り直してもう片方のコマンドを実行すると成功したので、仮に違う方のコマンドを実行しても問題ないかな、と思います（おそらく）。

## 番外編
ちなみに、私は超小型のUSBメモリを以下のようにして使っています。

常時つけっぱなしにできるので、パソコン側の記憶領域が足りなかったり、バックアップをしたいときに便利です。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1580351708/Blog-personal/Ubuntu_on_USB_does_not_start/USB_memory.jpg"  alt="USBメモリ" caption="USBメモリ" >}}

*追記*

この方法をやっていると、そのうちに高負荷をかけたときに認識しなくなり、最後はまったく認識しなくなりました。
おそらく、パソコン側の熱の影響を受けたんじゃないかな、と思います。
超小型は、それなりに耐久性に心配があるので、最悪消えても割り切れる使い方をしたほうが良いです。

というか、データは時間をかけた努力の成果です。1箇所だけに保存するのは危険です（人のこと言えない）。
