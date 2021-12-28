---
title: "ThunderbirdでExchange OnlineをOAuth 2.0認証する"
date: 2021-02-03T17:02:33+09:00
lastmod: 2021-02-03T17:02:33+09:00
author: "たかめろん"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1609052102/Blog-personal/thunderbird_exchange_online/6.png"]
categories: ["ソフトウェア・サービス"]
tags: []
archives: ["2021", "2021-02"]
toc: false
draft: false
---

Microsoft 365（旧：Office365）には、メール機能(Exchange Online, Outlook）が付属しています。
[Exchange Onlineの基本認証（レガシ認証）は廃止となる](https://docs.microsoft.com/ja-jp/lifecycle/announcements/exchange-online-basic-auth-deprecated "Exchange Online の基本認証が非推奨となります | Microsoft Docs")予定であり、現在も[セキュリティの既定値群](https://docs.microsoft.com/ja-jp/azure/active-directory/fundamentals/concept-fundamentals-security-defaults "Azure Active Directory のセキュリティ デフォルト | Microsoft Docs")が設定されていると基本認証が無効になります。
基本認証にはIMAP、SMTP、POP3といったメールプロトコルが含まれ、メールアプリでこれらのプロトコルを利用してExchange Onlineを利用している方は利用できなくなります。

そして、[Exchange Onlineが先進認証の一つであるOAuth 2.0に対応](https://techcommunity.microsoft.com/t5/exchange-team-blog/announcing-oauth-2-0-support-for-imap-and-smtp-auth-protocols-in/ba-p/1330432 "Announcing OAuth 2.0 support for IMAP and SMTP AUTH protocols in Exchange Online - Microsoft Tech Community")しました。そこで、ThunderbirdでExchange OnlineをOAuth 2.0認証で利用する方法を紹介します。
Thunderbirdで「Exchange用のフクロウ」というアドオンを利用している方も、本ページで紹介する方法のほうが高機能であり、何より無料です。

**利点**

- 2段階認証を設定していても使える  
    　アプリパスワードは不要です
- Thunderbirdの機能をすべて使える  
    　Outlook Web Access (OWA) を使用する「Exchange用のフクロウ」というアドオンでは送受信くらいしかできません

## 手順

最初に、送信者名・メールアドレス・パスワードを入力します。
「パスワードを記憶する」にチェックを入れると、メールの送受信時に認証を求められなくなります。
入力し終わったら「続ける」ボタンをクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1609052102/Blog-personal/thunderbird_exchange_online/1.png"  alt="" caption="" >}}

Thunderbirdが自動で接続設定を見つけてくれますが、基本認証になっています。
「手動設定」ボタンをクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1609052102/Blog-personal/thunderbird_exchange_online/2.png"  alt="" caption="" >}}

このような画面になります。ユーザー名にはメールアドレスが入力されているはずです。
共有メールボックスのアドレスを使う場合は、以下の通りに設定してください。

メールアドレスが以下だとします。  
| 用途             | メールアドレス       |
| :---: | :---: |
| メイン           | main@example.com  |
| 共有メールボックス | share@example.com |

ユーザー名を以下の通りに設定してください。  
| サーバ          | ユーザー名          |
| :---: | :---: |
| 受信サーバ(IMAP) | share@example.com |
| 送信サーバ(SMTP) | main@example.com  |

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1609052102/Blog-personal/thunderbird_exchange_online/3.png"  alt="" caption="" >}}

次に、認証方法を「OAuth2」に設定します。
これで「完了」ボタンをクリックします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1609052102/Blog-personal/thunderbird_exchange_online/4.png"  alt="" caption="" >}}

ログインが求められます。
共有メールボックスの場合は、共有メールボックスのアドレスでパスワードが求められます。
メインのアドレスのパスワードを利用したい場合は、「別のアカウントでサインインする」をクリックし、メインのアドレスを入力してログインします。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1609052102/Blog-personal/thunderbird_exchange_online/5.png"  alt="" caption="" >}}

Thunderbirdにアクセス許可をします。
ここで「承諾」ボタンをクリックすると、Thunderbirdに戻り、アカウントが登録されます。
何かしらの警告が表示されていた場合は、とりあえず「完了」ボタンをクリックしてみてください。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1609052102/Blog-personal/thunderbird_exchange_online/6.png"  alt="" caption="" >}}
