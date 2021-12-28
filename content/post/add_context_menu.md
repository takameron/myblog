---
title: "右クリックメニューにプログラムを追加"
date: 2020-06-08T14:54:11+09:00
lastmod: 2020-06-08T14:54:11+09:00
author: "たかめろん"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1584782117/Blog-personal/add_context_menu/thumb.png"]
categories: ["Tips"]
tags: []
archives: ["2020", "2020-06"]
toc: true
draft: false
---

右クリックメニュー（コンテキストメニュー）にソフトウェアを追加しておけば、たまにこのソフトウェアでファイルを開きたい！というときに便利ですよね。

今回は、サクラエディタをアイコン付きでコンテキストメニューに追加する方法を紹介します。

{{< warning >}}
この作業では **レジストリの改変** をおこないます。
間違ったキーを削除したり名前を変更してしまうことのないよう、ご注意ください。
{{< /warning >}}

## レジストリエディターを起動

「Windowsキー」と「Rキー」を同時に押して、「ファイル名を指定して実行」を表示させます。
「名前」欄に「regedit」と入力してEnterキーを押すと、ユーザーアカウント制御のメッセージが出た後に、レジストリエディターが起動します。
（ユーザーアカウント制御を突破するには管理者権限が必要です。）

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782116/Blog-personal/add_context_menu/1_execute.png" img_w=399 img_h=206 w=399 form="landscape" alt="「ファイル名を指定して実行」で「regedit」と入力" caption="" >}}

レジストリエディターが起動しました！
キーは階層構造になっており、左ペインでキーをたどり、右ペインで値の操作をします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782117/Blog-personal/add_context_menu/2_regedit.png"  alt="レジストリエディター" caption="" >}}

## バックアップを取る

最悪レジストリが壊れても復旧できるように、バックアップを取ります。

メニューバーの「ファイル」→「エクスポート」を選択します。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782117/Blog-personal/add_context_menu/3_export1.png"  alt="レジストリエディターのメニューバーから「ファイル」→「エクスポート」" caption="" >}}

バックアップファイルを保存するフォルダを選択してください。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782117/Blog-personal/add_context_menu/4_export2.png"  alt="バックアップファイルを保存するフォルダを選択" caption="" >}}

ファイル名を入力してください。

「保存」ボタンをクリックすると、指定したフォルダ内に拡張子が「.reg」で終わるファイルが出来ています。
レジストリをバックアップ時点に戻したい場合は、このファイルをダブルクリックして実行します。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782117/Blog-personal/add_context_menu/5_export3.png"  alt="バックアップファイル名を入力" caption="" >}}

## コンテキストメニューに追加

ではいよいよ、コンテキストメニューにソフトウェアを追加します！

左ペインで「HKEY_CLASSES_ROOT」→「*」→「shell」をたどっていきます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782117/Blog-personal/add_context_menu/6_open.png"  alt="キーをたどっていく" caption="" >}}

「shell」キーを右クリックし、「新規」→「キー」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782117/Blog-personal/add_context_menu/7.png"  alt="「shell」キーのサブキーを作成" caption="" >}}

キーの名称には、わかりやすい名称をつけておきます。

（このスクリーンショットは後から撮ったもので、すでにサクラエディタ用に「Sakura」というキーを作ってありました。というわけで、ここでは「Hoge」というキー名にします(^^;)）

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782117/Blog-personal/add_context_menu/8.png"  alt="サブキーの作成完了" caption="" >}}

キーを作成すると、右ペインに「(規定)」という名称の値があります。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782118/Blog-personal/add_context_menu/9.png"  alt="右ペインに「(規定)」という値があることを確認" caption="" >}}

「(規定)」という値を右クリックし、「編集」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782118/Blog-personal/add_context_menu/10.png"  alt="「(規定)」という値を編集" caption="" >}}

「値のデータ」欄に、コンテキストメニューに追加したい文字列を入力します。

「(&M)」のように入力すると、右クリックしてコンテキストメニューを表示した後にMキーを押すと、自動でこの項目が選択されます。

入力を終えたら「OK」ボタンをクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782118/Blog-personal/add_context_menu/11.png" img_w=443 img_h=190 w=443 form="landscape" alt="コンテキストメニューに表示する文字列を指定" caption="" >}}

このようになりました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782118/Blog-personal/add_context_menu/12.png"  alt="コンテキストメニューに表示する文字列の指定完了" caption="" >}}

次は、ソフトウェアのパスを登録していきます。

先ほど作成したキー（ここでは「Hoge」）を右クリックし、「新規」→「キー」をクリックします。
キーの名称は「command」にします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782118/Blog-personal/add_context_menu/13.png"  alt="「command」というサブキーを作成" caption="" >}}

再び「(規定)」という値を右クリックし、「編集」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782118/Blog-personal/add_context_menu/14.png"  alt="「command」キーの「(規定)」の値を編集" caption="" >}}

ソフトウェアのパスを入力します。
パスに空白が含まれていても、""（ダブルクォーテーション）で囲う必要はありません。

「%1」と入力すると、「%1」の箇所が右クリックしたときのファイルのパスに置き換えられます。
ソフトウェアが、右クリックしたファイルを開いた状態で起動するようになります。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782118/Blog-personal/add_context_menu/15.png" img_w=443 img_h=190 w=443 form="landscape" alt="ソフトウェアのパスを入力" caption="" >}}

このようになりました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782118/Blog-personal/add_context_menu/16.png"  alt="ソフトウェアのパス入力完了" caption="" >}}

さて、ここで適当なファイルを右クリックしてコンテキストメニューを表示すると、「〇〇で開く(M)」という項目が追加されていることが確認できます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782118/Blog-personal/add_context_menu/17.png" img_w=496 img_h=309 w=496 form="landscape" alt="コンテキストメニューの確認" caption="" >}}

## アイコンの追加

項目にはアイコンを表示できます。

最初に作成したキー（ここでは「Hoge」キー）を選択します。
右ペインで空白部分を右クリックし、「新規」→「文字列値」をクリックします。

名称は「Icon」にします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782118/Blog-personal/add_context_menu/18.png"  alt="「Icon」という値を作成" caption="" >}}

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782118/Blog-personal/add_context_menu/19.png"  alt="「Icon」という値を作成の完了" caption="" >}}

「Icon」を右クリックし、「修正」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782118/Blog-personal/add_context_menu/20.png"  alt="「Icon」という値を編集" caption="" >}}

ソフトウェアのパスを登録すると、そのソフトウェアのアイコンが表示されるようになります。

「値のデータ」欄に、ソフトウェアのパスを入力します。""（ダブルクォーテーション）で囲う必要はありません。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782119/Blog-personal/add_context_menu/21.png" img_w=443 img_h=190 w=443 form="landscape" alt="ソフトウェアのパスを入力" caption="" >}}

このようになりました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782119/Blog-personal/add_context_menu/22.png"  alt="ソフトウェアのパスを入力の完了" caption="" >}}

さて、実際に適当なファイルを右クリックしコンテキストメニューを表示すると、アイコン付きで「〇〇を開く(M)」という項目が追加されていることが確認できます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782117/Blog-personal/add_context_menu/23.png" img_w=595 img_h=350 w=595 form="landscape" alt="コンテキストメニューの確認" caption="" >}}

これで作業は終了です。
レジストリエディターは終了して大丈夫です。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584782117/Blog-personal/add_context_menu/24.png"  alt="レジストリエディターの終了" caption="" >}}
