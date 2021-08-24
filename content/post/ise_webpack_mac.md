---
title: "MacでISE WebPackを使う"
date: 2021-08-24T18:06:31+09:00
lastmod: 2021-08-24T18:06:31+09:00
author: "ぶっち"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1629775984/Blog-personal/ise_webpack_mac/thumb.png"]
categories: ["電子工作"]
tags: ["FPGA"]
archives: ["2021", "2021-08"]
toc: true
draft: false
---

ISE WebPACKをMacで動かす方法を紹介します。

手順は以下の順番です。
1. VirtualBoxでUbuntuの仮想マシンを作成
1. ISE WebPackのインストール
1. USBドライバのインストール

環境は以下のとおりです。

| | |
| --- | --- |
| パソコン | MacBook Pro (13-inch, 2020, Four Thunderbolt 3 ports) |
| OS | macOS Big Sur 11.5.2 |
| FPGA | SPARTAN-6 XC6SLX9 TQG144 |
| ダウンロードケーブル | [Digilent XUP USB-JTAG](https://digilent.com/xup-usb-jtag-programming-cable/ "XUP USB-JTAG Programming Cable - Digilent") |

## Ubuntuの仮想マシンを作成

| ソフトウェア | バージョン |
| --- | --- |
| VirtualBox | 6.1.26 r145957 (Qt5.6.3) |
| Ubuntu | Ubuntu Desktop 20.04.2.0 LTS |

最初にVirtualBoxをインストールします。[公式サイト](https://www.virtualbox.org/wiki/Downloads "Downloads – Oracle VM VirtualBox")からダウンロードしたり、Homebrewを使ったりしてインストールしてください。

次にUbuntuを[公式サイト](https://jp.ubuntu.com/download "Ubuntuを入手する | Ubuntu | Ubuntu")からダウンロードしてください。

仮想マシンを作成します。適当に作成すればよいですが、今回は以下の設定にしました。ディスクは、アップデートを諸々適用してISE WebPACKを使える状態で50GB程度使っているので、大きめにとった方が良さそうです。

| 項目 | 設定値 |
| --- | --- |
| 名前        | Ubuntu |
| タイプ      | Linux |
| バージョン   | Ubuntu (64-bit) |
| メモリ      | 4096MB |
| 仮想ディスク | VDI 可変サイズ 100.00GB |

仮想マシンの作成が完了したら、設定を開きます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629775988/Blog-personal/ise_webpack_mac/ubuntu-install1.png" alt="仮想マシンの設定を開く" caption="仮想マシンを選択し、上部の「設定」をクリック" >}}

「ストレージ」→「コントローラー: IDE」→「空」を選択します。右側のディスクマークから「ディスクファイルを選択」をクリックし、Ubuntuのイメージファイルを選択します。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629775988/Blog-personal/ise_webpack_mac/ubuntu-install2.png" alt="仮想マシンの設定でUbuntuのイメージファイルを選択" caption="Ubuntuのイメージファイルを挿入する" >}}

選択したら、右下の「OK」ボタンをクリックし、設定を保存します。

その後は仮想マシンを起動し、画面に沿ってUbuntuをインストールしてください。

## ISE WebPACKとライセンスファイルのダウンロード

最初にISE WebPACKをダウンロードします。[ダウンロードページ](https://japan.xilinx.com/downloadNav/vivado-design-tools/archive-ise.html "ISE ダウンロード アーカイブ ページ：3X - 14X")を開き、「14x」→「14.7」→「ISE Design Suite - 14.7  Full Product Installation」を開いていき、「Linux用フルインストーラー」をクリックしてください。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629776848/Blog-personal/ise_webpack_mac/ise_download1.png" alt="Linux用のISE WebPACKをダウンロード" caption="「Linux用フルインストーラー」をクリック" >}}

氏名や住所を入力する画面になるので、項目を埋めていきます。最後に「Download」ボタンをクリックすると、ダウンロードが始まります。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629776848/Blog-personal/ise_webpack_mac/ise_download2.png" alt="氏名・住所の入力" caption="指示どおりに氏名や住所などの入力" >}}

次にライセンスファイルを取得します。[Licensing Site](http://www.xilinx.com/getlicense/)にアクセスすると、先ほどと同様に氏名や住所を尋ねられるので、項目を埋めます。埋め終わったら「Next」をクリックします。

「Manage Licenses」タブを選択し、青色になっている箇所をダブルクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629776848/Blog-personal/ise_webpack_mac/license_download1.png" alt="Manage Licensesを開く" caption="Manage Licensesを開く" >}}

「ISE WebPACK License」にチェックを入れ、下部の「Next」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629776848/Blog-personal/ise_webpack_mac/license_download2.png" alt="Manage Licensesを開く" caption="Manage Licensesを開く" >}}

あとは流れを追えませんでしたが、なんだかんだで「Xilinx.lic」というライセンスファイルを取得できるはずです。

## Guest Additionsのインストール
ホストマシンとゲストマシンの間でドラッグドロップをしたりクリップボードの共有をしたりするため、ゲストマシンにGuest Additionsをインストールします。

Guest Additionsを導入するのに必要なソフトウェアをインストールするため、端末を起動して以下のコマンドを実行します。パスワードを求められるので、入力します。
```sh {linenos=false}
sudo apt install gcc make perl
```

仮想マシンのウィンドウをアクティブにした状態で、「Devices」→「Insert Guest Additions CD image」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629778751/Blog-personal/ise_webpack_mac/GuestAdditions1.png" alt="Guest Additionsのイメージを挿入" caption="「Insert Guest Additions CD image」をクリック" >}}

以下のような表示があったら「実行」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629778751/Blog-personal/ise_webpack_mac/GuestAdditions2.png" alt="Guest Additionsのインストール" caption="「実行」をクリック" >}}

このような表示がなければ、端末から以下のようなコマンド（[ユーザ名]と[バージョン]は適宜当てはめてください）を実行してください。

```sh {linenos=false}
sudo /media/[ユーザ名]/VBox_GAs_[バージョン]/VBoxLinuxAdditions.run
```

## ISE WebPACKのインストール
「Drag and Drop」→「Bidirectional」をクリックして、ホストマシンとゲストマシンが相互にドラッグ・アンド・ドロップをできるようにします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629780591/Blog-personal/ise_webpack_mac/dragdrop.png" alt="ドラッグアンドドロップを双方向にする" caption="「Drag and Drop」→「Bidirectional」をクリック" >}}

次に、ホストマシンからゲストマシンへ「Xilinx_ISE_DS_Lin_14.7_1015_1.tar」と「Xilinx.lic」をコピーします。

ここで端末を起動してください。
インストーラを起動するのに必要なソフトウェアをインストールします。
```sh {linenos=false}
sudo apt install libncurses5
```

以下の通りにコマンドを実行していきます。[ファイルを置いたところ]は、「Xilinx_ISE_DS_Lin_14.7_1015_1.tar」と「Xilinx.lic」をコピーしたディレクトリのパスです。

```sh
cd [ファイルを置いたところ]
tar -xvf Xilinx_ISE_DS_Lin_14.7_1015_1.tar
cd Xilinx_ISE_DS_Lin_14.7_1015_1
sudo ./xsetup
```

インストーラが起動します。「Next >」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629794519/Blog-personal/ise_webpack_mac/ise1.png" alt="インストーラの起動画面" caption="インストーラの起動画面" >}}

同意するか尋ねられるので、同意できるならチェックを2箇所入れます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629794519/Blog-personal/ise_webpack_mac/ise2.png" alt="ライセンスの同意1つ目" caption="よく読んで同意事項に同意1" >}}

同意するか尋ねられるので、同意できるならチェックを1箇所入れます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629794519/Blog-personal/ise_webpack_mac/ise3.png" alt="ライセンスの同意2つ目" caption="よく読んで同意事項に同意2" >}}

今回は「ISE WebPACK」をインストールするので、「ISE WebPACK」を選択します。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629794519/Blog-personal/ise_webpack_mac/ise4.png" alt="インストールするプロダクトを選択" caption="「ISE WebPACK」を選択" >}}

オプション機能では、後に別途USBドライバをインストールするので標準のままでよいと思いますが、念の為「Install Cable Drivers」にもチェックを入れます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629794519/Blog-personal/ise_webpack_mac/ise5.png" alt="インストールするオプション機能を選択" caption="一応「Install Cable Drivers」も選択" >}}

インストール先は標準のままで大丈夫です。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629794519/Blog-personal/ise_webpack_mac/ise6.png" alt="インストール先ディレクトリを設定" caption="インストール先ディレクトリはそのまま" >}}

インストール内容の確認です。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629794519/Blog-personal/ise_webpack_mac/ise7.png" alt="インストール内容の確認" caption="インストール内容の確認" >}}

インストールが始まります。10数分くらい時間がかかります。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629794519/Blog-personal/ise_webpack_mac/ise8.png" alt="インストール中" caption="インストール中" >}}

USBドライバのインストールに失敗したというメッセージが表示されました。気にしなくて大丈夫です。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629794519/Blog-personal/ise_webpack_mac/ise9.png" alt="USBドライバのインストールに失敗" caption="USBドライバのインストールに失敗" >}}

インストールが完了しました！

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629794519/Blog-personal/ise_webpack_mac/ise10.png" alt="インストール完了" caption="インストール完了" >}}


## USBドライバのインストール

USBドライバのインストールをします。端末で以下のコマンドを順に実行してください。

```sh
sudo apt install git libusb-dev fxload
cd /opt/Xilinx
sudo git clone git://git.zerfleddert.de/usb-driver
cd usb-driver/
sudo make
./setup_pcusb /opt/Xilinx/14.7/ISE_DS/ISE
sudo udevadm control --reload-rules
```

```.bashrc```の末尾に以下を追加します。
```sh {linenos=false}
. /opt/Xilinx/14.7/ISE_DS/settings64.sh
export LD_PRELOAD=/opt/Xilinx/usb-driver/libusb-driver.so
```

最後に```.bashrc```の変更を反映させるため、端末で以下のコマンドを実行します。
```sh {linenos=false}
. ~/.bashrc
```

これでISE WebPACKを使えるようになりました。
端末で```ise```コマンドを実行するとProject Navigatorが起動し、```planAhead```コマンドを実行するとplanAheadが起動します。

ちなみに、```.bashrc```に書き込む代わりに、以下のような起動用のシェルスクリプトを作成しても良いかもしれません。
```sh {linenos=false}
#!/bin/bash
. /opt/Xilinx/14.7/ISE_DS/settings64.sh
export LD_PRELOAD=/opt/Xilinx/usb-driver/libusb-driver.so
ise
```

## ライセンス登録
初回起動時にはライセンスの確認が行われ、エラーが表示されます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629790098/Blog-personal/ise_webpack_mac/license1.png" alt="ISEのライセンスが見つからないというエラー" caption="ISEのライセンスが見つからないというエラー" >}}

以下のウィンドウが現れるので、「Manage Licenses」→「Load License」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629790098/Blog-personal/ise_webpack_mac/license2.png" alt="ライセンスファイルを読み込む" caption="「Manage Licenses」→「Load License」をクリック" >}}

ライセンスファイルを指定します。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629790098/Blog-personal/ise_webpack_mac/license3.png" alt="ライセンスファイルの指定" caption="ライセンスファイルを選択する" >}}

ライセンスの確認ができました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629790098/Blog-personal/ise_webpack_mac/license4.png" alt="ライセンスのインストールが成功" caption="ライセンスの確認に成功" >}}


## ダウンロード
ダウンロードケーブルをパソコンと接続します。ケーブルはUSB Type-Aですが、MacはUSB Type-Cしかありませんので、アダプタを使います。感覚的に、複数種類に変換できる変換器のようなものではなく、下の写真のように単純にUSB Type-A Type-C 間の変換を行うアダプタの方が安定すると思います。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629785795/Blog-personal/ise_webpack_mac/adapter.jpg" alt="USB Type-A Type-C　アダプタ" caption="USB Type-A Type-C　アダプタ" >}}

ダウンロードケーブルをゲストマシンに接続します。「Devices」→「USB」→「Xilinx, Inc.」をクリックします。「Xilinx, Inc.」は違う名称になっている可能性がありますが、それっぽいもの（「Xilinx」の文字があるなど）をクリックしてください。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629785375/Blog-personal/ise_webpack_mac/download1.png" alt="Xilinxデバイスの選択" caption="Xilinxデバイスの選択" >}}

実はダウンロードケーブルとの接続が何回か切れてしまい、その度に接続し直していました。最終的に「XILINX」にチェックが入っている状態でダウンロードに成功しました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629794350/Blog-personal/ise_webpack_mac/download2.png" alt="Xilinxデバイスの選択" caption="Xilinxデバイスの選択" >}}

これで、ダウンロードができるようになりました！

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629784469/Blog-personal/ise_webpack_mac/done.png" alt="ダウンロード完了" caption="ダウンロード完了" >}}


## あとがき
ここにたどり着くまでに紆余曲折がありました。どの方法でもProject Navigatorは起動しますが、最後のFPGAへのダウンロードに失敗してしまうことばかりでした。

まず、仮想環境御三家とも言える以下の3ソフトを試しました。

* Parallels Desktop 16
* VMWARE FUSION Player 12
* VirtualBox

ParallelsにWindows 10をインストールしてみると仮想マシンにデバイスは認識されているものの、iMPACTでダウンロードケーブルが認識されませんでした。
VMWAREやVirtualBoxでCentOSなどを試してみても、ネット上の情報は古いものが多かったりサイトによって書いてあることが違ったりして、Project Navigatorを起動させるだけで精一杯でした。
ちなみに、今回はゲストOSにUbuntuを使いましたが、Lubuntuを使うとインストーラから画像やラジオボタンが消え、操作不可能でした。

次にCrossOverのオープンソース版を試しましたが、ISE WebPACKは複数のソフトウェアが協調して成り立っているため、うまく行きませんでした。

というわけで、今回はWebサイトを見て回って、うまくいった例を紹介しています。

また、ブートキャンプでインストールしたWindows 10だとダウンロードができた、という話を聞いたことがありますので、この方法だとWindows 10からISE WebPACKを使えるかもしれません。

### 参考サイト
* [Install xilinx platform usb in Ubuntu 16.04 x64 - Ask Ubuntu](https://askubuntu.com/questions/838260/install-xilinx-platform-usb-in-ubuntu-16-04-x64 "Install xilinx platform usb in Ubuntu 16.04 x64 - Ask Ubuntu")
* [Hello FPGA — Xilinx ISE setup on Ubuntu | by Antoine C. | Medium](https://antc2lt.medium.com/hello-fpga-nexys-3-setup-on-ubuntu-ff58e774566b "Hello FPGA — Xilinx ISE setup on Ubuntu | by Antoine C. | Medium")
* [Xilinx ISE Design Suite 14.7 を Ubuntu 14.04 にインストールする](http://cellspe.matrix.jp/parallella/inst_ise.html "Xilinx ISE Design Suite 14.7 を Ubuntu 14.04 にインストールする")
