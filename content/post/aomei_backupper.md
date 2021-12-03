---
title: "AOMEI Backupperでまるごとバックアップ"
date: 2021-12-01T22:01:00+09:00
lastmod: 2021-12-03T18:32:00+09:00
author: "ぶっち"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1638145507/Blog-personal/aomei_backupper/top1.png"]
categories: ["ソフトウェア・サービス"]
tags: ["レビュー"]
archives: ["2021","2021-12"]
toc: true
draft: false
---

『AOMEI Backupper』というバックアップソフトを紹介します！

<!--more-->

{{< blogcard "https://www.ubackup.com/jp/" >}}

{{< warning >}}
本記事はレビュー記事です。記事依頼を受け、AOMEI Backupper Professional版の提供を受けています。
{{< /warning >}}

バックアップ、重要なのはわかっているけれど今は困っていないしいいや、なんて思うことありませんか？

バックアップにはいろいろな方法があり、それぞれメリット・デメリットがあります。
まるごとバックアップしようと思うと大掛かりになりがちで、いろいろな知識を必要とされたり面倒だったりします。

今回は無料で使える「AOMEI Backupper Standard版」をレビューします。

{{< info >}}
本記事は「AOMEI Backupper Standard版」（バージョン 6.7.0）に基づいています。
2021年12月1日時点の情報ですので、今後のアップデートにより本記事の内容とは異なる可能性があります。
{{< /info >}}

## 無料版でできること
『AOMEI Backupper』には複数のエディションがあり、以下のサイトで特徴と価格を確認できます。

{{< blogcard "https://www.ubackup.com/jp/edition-comparison.html" >}}

バックアップは、無料版でもディスクやパーティション単位でバックアップでき、機能は十分です。
有料版になると差分バックアップ、バックアップイメージの暗号化や分割ができるようになります。
とりあえず手元の状態を保存するなら無料版で十分であり、継続的にバックアップをしたり重要な情報を保護したい場合は有料版をオススメします。

同期機能は、無料版では手動または自動（スケジュールなのかな？）で「Aフォルダ」から「Bフォルダ」の向きで同期する「ベーシック同期」を利用できます（ファイルの削除も追従する）。
有料版になると、「Aフォルダ」と「Bフォルダ」の双方向で同期する「双方向同期」、「Aフォルダ」と「Bフォルダ」の内容を同一にする「ミラー同期」、ファイルやフォルダの変更を検知して自動で同期する「リアルタイム同期」を利用できます。

復元機能は、無料版でもバックアップと同様にファイル、システム、ディスク、パーティション単位で復元できます。
有料版になると、「ユニバーサル復元」を利用できるようになり、異なるハードウェアで構成された別コンピュータに復元できるそうです。
また、物理コンピュータのバックアップから仮想マシンを作ることができるようです。
これは便利そう！

クローン機能では、無料版では制限付きで[ディスクのクローン](https://www.ubackup.com/jp/help/disk-clone.html?utm_source=article&utm_medium=anchor&utm_campaign=takameron&utm_content=anchor-ly-20211202)ができ、またパーティションとセクタ単位でクローンできます。
有料版になるとディスクのクローンの制限がなくなり、「パーティションのサイズ調整」を利用できたり、小さい容量のディスクから大きい容量のディスクへクローンするときに全パーティションに空き容量を追加することができます。

ツールでは、無料版では「回復環境の作成」を利用でき、システムがクラッシュしたとき用にバックアップ・復元を実行できる回復環境をWindowsのブートオプションメニューに追加するそうです。
また、バックアップイメージの圧縮・チェックなどもできます。
有料版になると、バックアップイメージの合併、マウントをできるよになるそうです。
「バックアップイメージをマウント」は需要がありそう！

## インストール
以下からダウンロードできます。

{{< blogcard "https://www.ubackup.com/jp/download.html" >}}

ダウンロードしたインストーラーを起動すると、ユーザーアカウント制御を求められます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145506/Blog-personal/aomei_backupper/install1.png" alt="ユーザーアカウント制御" caption="ユーザーアカウント制御" >}}

インストーラーの使用言語はWindowsに設定されているものがデフォルトでセットされています。
今回は「Japanese（日本語）」のまま「OK」ボタンをクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145506/Blog-personal/aomei_backupper/install2.png" alt="言語の選択で「Japanese（日本語）」を選択" caption="言語の選択" >}}

AOMEI Backupper Professional版の無料体験を勧められます。
今回は「スキップ」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145506/Blog-personal/aomei_backupper/install3.png" alt="AOMEI Backupper Pro版の紹介ウィンドウ" caption="Pro版を勧められる" >}}

インストールしていきます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145506/Blog-personal/aomei_backupper/install4.png" alt="インストール開始" caption="「今すぐインストール」をクリック" >}}

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145506/Blog-personal/aomei_backupper/install5.png" alt="インストール中" caption="しばらく待つ" >}}

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145506/Blog-personal/aomei_backupper/install6.png" alt="インストール終了" caption="「今すぐ体験」をクリック" >}}

<!-- {{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145507/Blog-personal/aomei_backupper/install7.png" alt="" caption="" >}} -->

インストールが終わりました。

どんな機能があるのか見ていきましょう！  
機能名の隣に黄色の丸いものがついている場合は、有料版だけの機能です。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145507/Blog-personal/aomei_backupper/top1.png" alt="ホーム画面" caption="ホーム" >}}

バックアップには「システムバックアップ」「ディスクバックアップ」「ファイルバックアップ」「パーティションバックアップ」などがあります。
つまり、ファイルやフォルダを個別でも、CドライブやDドライブといったドライブ単位でも、HDDやSSDまるごとでも、バックアップできます。

まるごとバックアップしておけばバックアップし忘れた、なんてことがないため、時間はかかりますが安心感が高まります。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145507/Blog-personal/aomei_backupper/top2.png" alt="バックアップメニュー" caption="バックアップ" >}}

同期では、無料版では「ベーシック同期」というものを使えます。
詳しくは知りません…

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145507/Blog-personal/aomei_backupper/top3.png" alt="同期メニュー" caption="同期" >}}

このソフトウェアでバックアップすると、こちらにバックアップ一覧が表示されます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145507/Blog-personal/aomei_backupper/top4.png" alt="復元メニュー" caption="復元" >}}

クローンでは、無料版では「ディスククローン」「パーティションクローン」をできるそうです。
HDDからSSDに換装するときに便利そうですね。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145507/Blog-personal/aomei_backupper/top5.png" alt="クローンメニュー" caption="クローン" >}}

ツール一覧です。

「Win11更新チェックツール」「ブータブルメディアの作成」「回復環境」「ディスク消去」「メール通知設定」「共有/NASデバイス管理」「ログ」「イメージをチェック」「配置をエクスポート/インポート」があります。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145507/Blog-personal/aomei_backupper/top6.png" alt="ツール一覧" caption="ツール1" >}}

「AOMEI Centralized Backupper」「AOMEI IneKey Recovery」「クラウドバックアップ」「AOMEI Partition Assistant」「システム最適化ツール」があります。

これらは普段から使うものではないですが、まれに必要なときがあります。
こういったユーティリティもあるのは便利ですね。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145508/Blog-personal/aomei_backupper/top7.png" alt="ツール一覧" caption="ツール2" >}}

## ディスクバックアップ
ディスクのバックアップを試してみました！

まずはバックアップ対象のディスクを選択します。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145499/Blog-personal/aomei_backupper/disk1.png" alt="ディスクバックアップ（ディスク選択前）" caption="ディスクを追加" >}}

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145499/Blog-personal/aomei_backupper/disk2.png" alt="ディスクバックアップ（ディスク選択後）" caption="ディスクを選択" >}}

右下の「開始 >>」ボタンをクリックし、バックアップを開始します。

ここで驚きましたが、バックアップ元のディスクと保存先のディスクは同一でもOKなんですね！
外付けHDDを工面しなくても良いというのはすごく便利です。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145499/Blog-personal/aomei_backupper/disk3.png" alt="ディスクバックアップ（バックアップ開始）" caption="バックアップ開始" >}}

しばらく待ちます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145499/Blog-personal/aomei_backupper/disk4.png" alt="ディスクバックアップ（ボリュームをバックアップ中）" caption="ボリュームをバックアップ中" >}}

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145500/Blog-personal/aomei_backupper/disk5.png" alt="ディスクバックアップ（データをバックアップ中）" caption="データをバックアップ中" >}}

<!-- {{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145499/Blog-personal/aomei_backupper/disk6.png" alt="" caption="" >}} -->

バックアップが完了しました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145499/Blog-personal/aomei_backupper/disk7.png" alt="ディスクバックアップ（バックアップ完了）" caption="バックアップ完了" >}}

エクスプローラーでバックアップファイルを確認すると、独自形式のバックアップファイルが生成されていました。
つまり『AOMEI Backupper』でしか開けないということなので、できればISO形式とか、汎用性のあるファイルだともっと嬉しかったかもですね…

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145500/Blog-personal/aomei_backupper/disk8.png" alt="ディスクバックアップ（エクスプローラーでバックアップファイルを表示）" caption="ディスクバックアップのバックアップファイル" >}}

「バックアップ管理」を見るとバックアップしたものが表示されています（システムバックアップを試したあとです）。
ハンバーガーメニューをクリックすると、このバックアップに対していろいろ操作できます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638173574/Blog-personal/aomei_backupper/disk9.png" alt="ディスクバックアップ（バッグアップ管理画面）" caption="ディスクバックアップ" >}}

復元は試していなくてごめんなさい(-_-;)

## システムバックアップ
システムバックアップも試してみました（正直ディスクバックアップとの違いはわかりません…）。

<!-- {{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145511/Blog-personal/aomei_backupper/system_backup1.png" alt="システムバックアップ（）" caption="" >}} -->

バックアップ先のみ指定できます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145512/Blog-personal/aomei_backupper/system_backup2.png" alt="システムバックアップ（バックアップ開始）" caption="バックアップ内容" >}}

<!-- {{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145512/Blog-personal/aomei_backupper/system_backup3.png" alt="システムバックアップ（）" caption="" >}} -->

しばらく待ちます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145512/Blog-personal/aomei_backupper/system_backup4.png" alt="システムバックアップ（バックアップ中）" caption="バックアップ中" >}}

バックアップが終わりました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145512/Blog-personal/aomei_backupper/system_backup5.png" alt="システムバックアップ（バックアップ完了）" caption="バックアップ完了" >}}

「操作は完了しました。」のところをクリックすると、操作内容を見られます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145511/Blog-personal/aomei_backupper/system_backup6.png" alt="システムバックアップ（履歴）" caption="操作履歴" >}}

<!-- {{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145513/Blog-personal/aomei_backupper/system_backup7.png" alt="システムバックアップ（バックアップ管理画面）" caption="" >}} -->

「バックアップ管理」を見るとバックアップしたものがあり、ハンバーガーメニューをクリックするといろいろな操作をできます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145516/Blog-personal/aomei_backupper/system_backup9.png" alt="システムバックアップ（バックアップ管理画面）" caption="システムバックアップ" >}}

バックアップするスケジュールを設定できます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145513/Blog-personal/aomei_backupper/system_backup10.png" alt="システムバックアップ（スケジュール）" caption="バックアップするスケジュール" >}}

エクスプローラーでバックアップファイルを確認すると、ディスクバックアップのときと同じように独自形式のファイルがありました。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145513/Blog-personal/aomei_backupper/system_backup8.png" alt="システムバックアップ（エクスプローラーでバックアップファイルを表示）" caption="システムバックアップのバックアップファイル" >}}

バックアップができたので、リカバリも見ていきます。

<!-- {{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145518/Blog-personal/aomei_backupper/system_recovery1.png" alt="バックアップ管理画面" caption="" >}} -->

ハンバーガーメニューをクリックして「復元」をクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145518/Blog-personal/aomei_backupper/system_recovery2.png" alt=システムバックアップの右クリックメニュー" caption="システムバックアップのコンテキストメニュー" >}}

システムまるごと復元と、パーティションごとに復元を選べるようです。
今回はシステムまるごとを選びます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145519/Blog-personal/aomei_backupper/system_recovery3.png" alt="復元するパーティションを選択" caption="パーティションを選択" >}}

復元先のパーティションを選びます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145520/Blog-personal/aomei_backupper/system_recovery4.png" alt="復元先を指定" caption="復元先を選択" >}}

ここで、容量不足で次に進めないことがわかりました。
ごめんなさい！

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1638145518/Blog-personal/aomei_backupper/system_recovery5.png" alt="復元先を選択したものの容量不足で「次へ」が押せない画面" caption="容量不足で次に進めなかった" >}}

## まとめ
『AOMEI Backupper』は、一時的に使うなら無料版でも十分で、継続的にしっかりとバックアップしたい場合は有料版がオススメであることがわかりました。

事故はいつ起こるかわかりません。HDDが壊れるかも、マルウェアに感染するかも、PCを紛失するかも、盗難に遭うかも…
保険と同じように、事故が起こった時に被害を抑えられるよう、こまめなバックアップをオススメします。

---

ちなみに、バックアップだけではなくクローンを作成する機能もあります。[ディスククローン](https://www.ubackup.com/jp/help/disk-clone.html?utm_source=article&utm_medium=anchor&utm_campaign=takameron&utm_content=anchor-ly-20211202)をご覧ください。
