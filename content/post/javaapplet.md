---
title: "UbuntuでJava Appletを動かす方法"
date: 2019-04-13T23:11:00+09:00
lastmod: 2019-04-13T23:11:00+09:00
author: "たかめろん"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1580351945/Blog-personal/thumbnail/programming.jpg"]
categories: ["プログラミング"]
tags: []
archives: ["2019", "2019-04"]
toc: true
draft: false
---

Ubuntu 18.04でJava Appletを動かすまでに多少手間がかかったので、メモを残します。

## 結論
先に結論です。

不正確な恐れもあるため、ファイルの削除などは自己責任で慎重に行ってください。  
バックアップをとっておくと安心です。

1. `openjdk-8-jdk`をインストール
```plain {linenos=false}
$ sudo apt install openjdk-8-jdk
```

2. `run.bat`やクラスファイルなど、自動で生成されるファイルを削除
3. `-Xlint:deprecation`オプションをつけてコンパイル
```plain {linenos=false}
$ javac -Xlint:deprecation Example.java
```

4. `appletviewer`コマンドで実行
```plain {linenos=false}
$ appletviewer play.html
```

## 動作させるまでの体験記
途中でターミナルを閉じてしまったので、最初のほうは言葉だけの説明になります。  
また、記載の順番が間違っているかもしれません（記憶を掘り起こしています）。

まず、`appletviewer`コマンドを入力すると、`openjdk-8-jdk`または `openjdk-11-jdk`というパッケージをインストールするように提案されます。

新しい方が良いと思い、 `openjdk-11-jdk`をインストール。
`appletviewer`コマンドを実行すると、以下のようなエラーメッセージが表示されて（抜粋です）、実行できません。

```plain {linenos=false}
java.security.AccessControlException: access denied
```

コンパイルをしてみると、まず以下のようなエラーメッセージが表示されます。

```plain {linenos=false}
$ javac Example.java
注意:Example.javaは推奨されないAPIを使用またはオーバーライドしています。
注意:詳細は、-Xlint:deprecationオプションを指定して再コンパイルしてください。
```

そこで、`-Xlint:deprecation`オプションをつけてコンパイルをすると、以下のようなエラーメッセージが表示されます。

```plain {linenos=false}
$ javac -Xlint:deprecation Example.java
Example.java:5: 警告:[deprecation] java.appletのAppletは推奨されません
public class Example extends Applet implements Runnable {
                                           ^
警告1個
```

どうにもならなくなったので、`openjdk-11-jdk`をアンインストールし、 `openjdk-8-jdk`をインストールしました。

再度、オプションをつけてコンパイルし、`appletviewer`コマンドを実行すると、またエラーメッセージが表示されました。

```plain {linenos=false}
$ appletviewer play.html
java.lang.UnsupportedClassVersionError: Example has been compiled by a more recent version of the Java Runtime (class file version 54.0), this version of the Java Runtime only recognizes class file versions up to 52.0
	at java.lang.ClassLoader.defineClass1(Native Method)
	at java.lang.ClassLoader.defineClass(ClassLoader.java:763)
	at java.security.SecureClassLoader.defineClass(SecureClassLoader.java:142)
	at sun.applet.AppletClassLoader.findClass(AppletClassLoader.java:217)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:424)
	at sun.applet.AppletClassLoader.loadClass(AppletClassLoader.java:152)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:357)
	at sun.applet.AppletClassLoader.loadCode(AppletClassLoader.java:626)
	at sun.applet.AppletPanel.createApplet(AppletPanel.java:801)
	at sun.applet.AppletPanel.runLoader(AppletPanel.java:730)
	at sun.applet.AppletPanel.run(AppletPanel.java:379)
	at java.lang.Thread.run(Thread.java:748)
```

`openjdk-11-jdk`をインストールしてコンパイルした名残のようです。
そこで、`run.bat`やクラスファイルなど、自動で生成されたと思われるファイルを削除して、再度コンパイルをしてみました。

そして、`appletviewer`コマンドを実行すると、きちんと動作しました！

## 雑感
Java AppletはJava9で非推奨になり、Java11で廃止になったそうです。

もはや使われなくなった、古いアプリケーションを実行するのは手間がかかりますね。
