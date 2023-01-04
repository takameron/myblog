---
title: "Thunderbirdで「user authenticated but not connected」というエラー"
date: 2023-01-04T19:08:02+09:00
lastmod: 2023-01-04T19:18:01+09:00
author: "たかめろん"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1672827432/Blog-personal/thunderbird_user_authenticated_but_not_connected/1.png"]
categories: ["ソフトウェア・サービス"]
tags: []
archives: ["2023","2023-01"]
toc: false
draft: false
---

2022年の終わりくらいから、ThunderbirdにてMicrosoft 365で契約しているメール（Microsoft Exchange Online）を読もうとすると、

> User is authenticated but not connected.

というエラーが発生したり、エラーが発生しなくても更新されていないなどの現象が発生しています。

Microsoft 365の設定はいじっていないし、Thunderbirdが自動更新された可能性はあるものの何もしていないしなぁと困っていましたが、下記のサイトの方法で解決しました。

* [Thunderbird IMAP responded: User is authenticated but not - Microsoft Community](https://answers.microsoft.com/en-us/outlook_com/forum/all/thunderbird-imap-responded-user-is-authenticated/062a82f6-e678-4462-88b7-dd6cc318386f)
* [Came back to Thunderbird after Christmas and now it won't connect? Authenticated but not connected. : Thunderbird](https://www.reddit.com/r/Thunderbird/comments/zxelqn/came_back_to_thunderbird_after_christmas_and_now/)

まず、設定から「設定エディター」を開きます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1672825631/Blog-personal/thunderbird_user_authenticated_but_not_connected/2.png" alt="設定にある「設定エディター」と書かれているボタン" caption="設定から「設定エディター」を開きます" >}}

「network.dns.disableIPv6」というワードで検索し、初期状態では **false** になっているので、 **true** に変更します。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1672825631/Blog-personal/thunderbird_user_authenticated_but_not_connected/3.png" alt="設定エディターにて network.dns.dis で検索した画面" caption="network.dns.disableIPv6 を true に変更する" >}}

念のためThunderbirdを再起動すると、正常に読み込まれるようになりました。

---

> User is authenticated but not connected.

というエラーは他にも下記のような原因など、いろいろ考えられます。
* 基本認証を使用している
    * 「通常のパスワード認証」を使用している → OAuth2を使うようにしましょう
* クライアントからのアクセスをブロックしている
    * https://admin.microsoft.com/ の「ユーザー」→「アクティブなユーザー」→ユーザを選択→「メール」→「メールアプリを管理する」にて、IMAPなどにチェックが入っていることを確認

今回は、2022年末から2023年始めにかけて発生したエラーの対処法を紹介しました。

やはり海外の掲示板や質問サイト、コミュニティの情報も拾えるようになると、問題の解決が早くなると感じました。
