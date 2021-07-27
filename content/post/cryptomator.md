---
title: "Cryptomatorでクラウドストレージのデータを暗号化する"
date: 2020-04-23T10:06:51+09:00
lastmod: 2020-04-23T11:00:07+09:00
author: "ぶっち"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1584423768/Blog-personal/cryptomator/thumb.png"]
categories: ["ソフトウェア・サービス"]
tags: ["セキュリティ"]
archives: ["2020", "2020-04"]
toc: true
draft: false
---

OneDrive Personal Vaultを使いたいと思ったのですが、Office 365 Businessでは使えません。代わりになるものを探すと、Cryptomatorというソフトウェアを見つけたので、ご紹介します。

## Cryptomatorとは？

クラウドストレージでの利用を考慮した、透過的に暗号化するフリーソフトウェアです。アカウント登録は無く、コンピュータにインストールして使います。Windows、macOS、Linux、Android、iOSに対応しています。

まずは、[公式サイト](https://cryptomator.org/ "Cryptomator - Free Cloud Encryption for Dropbox & Co")で紹介されている特徴を見てください！  
（重要なところは線を引きました）

良さそうですよね！

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423768/Blog-personal/cryptomator/24.png"  alt="公式サイトに書かれている特徴" caption="ソフトウェアの特徴" >}}

ソフトウェアで「金庫」と呼ばれるフォルダを作成し、ソフトウェアで解錠・施錠の操作をします。  
解錠すると仮想ドライブが作成され、その中に見かけは解錠済みのファイルやフォルダが入っています（ファイル名やフォルダ構造はわかるが、データは暗号化されている）。ファイルを開くと自動で復号化され、ファイルを保存すると自動で暗号化されるため、暗号化されていることを気にせずに使えます。  
ファイルを使い終わったら施錠をすると、仮想ドライブが消え、暗号化したデータが入っている「金庫」フォルダだけになります。

このように、透過的に暗号化がされます。また、ファイルの更新日時は暗号化されないため、クラウドストレージにおいて新しいデータが古いデータで上書きされることがないなど、クラウドストレージでの利用も考慮されています。

類似ソフトウェアとして、[Boxcryptor](https://www.boxcryptor.com/ "Encryption software to secure cloud files | Boxcryptor")、[CryptSync](https://www.gigafree.net/security/encrypt/CryptSync.html "CryptSync のダウンロードと使い方 - ｋ本的に無料ソフト・フリーソフト")、[CrococryptMirror](https://www.gigafree.net/security/encrypt/CrococryptMirror.html "CrococryptMirror のダウンロードと使い方 - ｋ本的に無料ソフト・フリーソフト")などがあります。
自動で暗号化・復号化をしてくれない非透過的でないか、ローカルだけでしか使えないタイプでないかなどに気をつけて選ぶと良いと思います。（あとは、ファイルを自動で送信するようなマルウェアでなく、信頼できるかどうか）

## 参考サイト

以下のサイトで詳しく紹介されているため、参考になります。

{{< blogcard "https://cryptomator.org/" >}}
{{< blogcard "https://excesssecurity.com/how-to-use-cryptomator/" >}}
{{< blogcard "https://blog.hitsujin.jp/entry/2019/05/15/120000" >}}

## 使ってみる

実際に使ってみます。

ダウンロードとインストールは、[公式サイト](https://cryptomator.org/downloads/ "Downloads")からダウンロードしてインストールするか、Chocolateyなどのパッケージマネージャーを使用してインストールします。

初回起動時には、ファイアウォールについてのウィンドウが表示されます。そもそもインターネットに繋ぐ必要があるのか疑問ですし、私の場合はキャンセルボタンを押しても正常に動作しました。
ここはお好みで設定して構わないと思います。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423766/Blog-personal/cryptomator/UAC.png"  alt="ファイアウォールの設定のウィンドウ" caption="ファイアウォールはお好みで設定" >}}

起動すると、このような画面になります。シンプルでわかりやすいですね。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423766/Blog-personal/cryptomator/1.png"  alt="メイン画面" caption="メイン画面" >}}

金庫フォルダを作成します。このフォルダの中に、暗号化されたデータや管理データが格納されます。

左下の「＋」ボタンをクリックし、「新しい金庫を作成」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423766/Blog-personal/cryptomator/2.png"  alt="「新しい金庫を作成」をクリック" caption="「新しい金庫を作成」をクリック" >}}

金庫フォルダを配置するフォルダに移動し、「ファイル名」の欄に金庫フォルダのフォルダ名を入力します。
ここでは「vault」（金庫という意味）というフォルダ名にしました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423766/Blog-personal/cryptomator/3.png"  alt="エクスプローラー画面で金庫フォルダを作りたいフォルダに移動し、金庫フォルダ名を入力" caption="金庫フォルダを作成" >}}

金庫フォルダにパスワードを設定します。
十分に複雑なものにしてください。
また、ここで設定したパスワードを忘れると、二度と金庫フォルダを開けなくなります。パスワードマネージャー（1Password, BitWardenなど）を使用するなどして、パスワードを紛失しないようにしてください。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423765/Blog-personal/cryptomator/4.png"  alt="金庫フォルダのパスワードを設定" caption="金庫フォルダのパスワードを設定" >}}

パスワード強度を評価してくれる機能があります。

パスワードを入力したら「金庫を作成」ボタンをクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423765/Blog-personal/cryptomator/5.png"  alt="パスワードを入力したら「金庫を作成」をクリック" caption="「金庫を作成」をクリック" >}}

金庫が作られました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423766/Blog-personal/cryptomator/6.png"  alt="パスワード入力画面" caption="パスワード入力画面" >}}

設定したパスワードを入力し、「金庫を解錠」ボタンをクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423766/Blog-personal/cryptomator/7.png"  alt="パスワードを入力し終わった画面" caption="「金庫を解錠」をクリック" >}}

金庫が解錠されました。

ソフトウェアでは、復号化・暗号化が行われると、その実行速度を見ることができます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423766/Blog-personal/cryptomator/8.png"  alt="解錠済み画面" caption="スループットを見ることができる" >}}

ソフトウェアのウィンドウは最小化できます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423767/Blog-personal/cryptomator/25.png"  alt="ウィンドウを最小化できる" caption="ウィンドウを最小化できる" >}}

金庫の解錠と同時に、仮想ドライブがエクスプローラーで開きます。
このドライブにファイルやフォルダを入れると、自動で暗号化・復号化が行われます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423767/Blog-personal/cryptomator/9.png"  alt="エクスプローラーで解錠済みの金庫フォルダを開いた画面" caption="エクスプローラーで解錠済みの金庫フォルダを開ける" >}}

エクスプローラーで見ると、仮想ドライブが作成されています。
ドライブ名は、金庫フォルダの名前になっています。
空き容量はパソコン本体のドライブと同じになっています。
クラウドストレージの容量と合致していないということは、クラウドストレージの容量がパソコンのストレージより大きいとき、クラウドストレージを使い切れないのかな？（未確認）

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423766/Blog-personal/cryptomator/10.png"  alt="仮想ドライブとして認識された解錠済み金庫フォルダ" caption="解錠済みの金庫フォルダは仮想ドライブとして認識されている" >}}

金庫を施錠すると、跡形もなく仮想ドライブが消えます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423766/Blog-personal/cryptomator/11.png"  alt="金庫フォルダを施錠すると仮想ドライブが消える" caption="金庫フォルダを施錠すると仮想ドライブが消える" >}}

実際にファイルを仮想ドライブに入れ、金庫フォルダ内を見てみました。

フォルダ構造とフォルダ名・ファイル名はわからないようになっています。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423767/Blog-personal/cryptomator/18.png"  alt="OneDriveから開いた金庫フォルダ" caption="ファイル名をフォルダ構造はわからない" >}}

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423767/Blog-personal/cryptomator/19.png"  alt="OneDriveから開いた金庫フォルダ" caption="ファイル名をフォルダ構造はわからない" >}}

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423767/Blog-personal/cryptomator/20.png"  alt="OneDriveから開いた金庫フォルダ" caption="ファイル名をフォルダ構造はわからない" >}}

ファイル名もわかりません。
ただ、ファイルサイズはわかるため、推測が可能かもしれません。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423767/Blog-personal/cryptomator/21.png"  alt="エクスプローラーで暗号化されたファイルを見てみる" caption="ファイル名は長くてわからないが、ファイルサイズがわかる" >}}

実は、解錠にあたって、オプションを設定することができます。

解錠をする画面で「オプションを表示」ボタンを押すとオプション一覧を見ることができます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423766/Blog-personal/cryptomator/12.png"  alt="オプション一覧" caption="オプション一覧" >}}

ドライブ文字を指定することができます。
「Z」など、なかなか使われなさそうなドライブ名にすると、金庫を解錠したあとは、ソフトウェアに残る履歴からファイルを開くことができます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423766/Blog-personal/cryptomator/13.png"  alt="仮想ドライブのドライブ文字は指定できる" caption="仮想ドライブのドライブ文字は指定できる" >}}

また、パスワードを保存するオプションもあります（未確認）。
おそらく、いちいちパスワードを入力せずとも、金庫を解錠できるようになると思います。
クラウドストレージで金庫を共有しているときなどに、特定のコンピュータからはパスワードを入力せずにスムーズに使いたいときに便利です。

また、パスワードを保存するオプションを有効にすると、起動時に解錠するオプションを選択可能になります。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423767/Blog-personal/cryptomator/14.png"  alt="パスワードを保存するオプションがある" caption="パスワードを保存するオプションがある" >}}

歯車のアイコンをクリックすると、ソフトウェアの設定画面になります。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423767/Blog-personal/cryptomator/15.png"  alt="ソフトウェアの設定画面" caption="ソフトウェアの設定画面" >}}

ソフトウェアのインストール時にDokanというライブラリをインストールしましたが、仮想ドライブのマウントに使われているようです。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423767/Blog-personal/cryptomator/16.png"  alt="マウント方法の選択" caption="マウント方法の選択" >}}

金庫を選択した状態でマイナス記号のボタンを押すと、金庫を一覧から削除できます。
ソフトウェア内のリストから削除されるだけで、金庫本体は削除されません。
金庫も削除する場合は、別途エクスプローラーなどから直接削除する必要があります。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423767/Blog-personal/cryptomator/17.png"  alt="金庫の削除" caption="金庫をリストから削除" >}}

リストから削除した金庫は、金庫フォルダが残っていれば、再度リストに追加することができます。

プラス記号のボタンを押して、「既存の金庫を開く」ボタンをクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423767/Blog-personal/cryptomator/22.png"  alt="金庫を開く" caption="リストに既存の金庫を追加する" >}}

「masterkey.cryptomator」というファイルを選択して、「開く」ボタンをクリックします。

これで、リストに追加されました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1584423767/Blog-personal/cryptomator/23.png"  alt="エクスプローラーで金庫フォルダを開く" caption="金庫フォルダ内の「masterkey.cryptomator」を選択" >}}

## まとめ

クラウドストレージが信用できない、万一流出しては困るデータがあるというときに、利便性とセキュリティを両立できるソフトウェアだと思います。

~~また、スマートフォン向けアプリがありますが、2020年3月21日現在、[Androidアプリ](https://play.google.com/store/apps/details?id=org.cryptomator "Cryptomator - Google Play のアプリ")は1,050円、[iOSアプリ](https://apps.apple.com/jp/app/cryptomator/id953086535 "‎「Cryptomator」をApp Storeで")は1,100円と、なかなか高価です。~~

2020年4月23日現在、Android・iOSともに600円になっていました。

まあ、フリーソフトなので、良いと思ったら、今後も開発を続けてもらって高品質なソフトウェアを使わせてもらえるように、寄付をすると良さそうです。
