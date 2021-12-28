---
title: "VSCodeでOpenGLのIntelliSenseを有効にする"
date: 2021-03-20T16:59:00+09:00
lastmod: 2021-03-20T16:59:00+09:00
author: "たかめろん"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1580351945/Blog-personal/thumbnail/programming.jpg"]
categories: ["プログラミング"]
tags: []
archives: ["2021", "2021-03"]
toc: false
draft: false
---

以下のページに従いOpenGLをインストールしました。

{{< blogcard "http://teacher.nagano-nct.ac.jp/ito/Springs_of_C/cyg64/index.html" >}}

Visual Studio Codeでコードを書くとOpenGL関連の関数にエラーが表示されました。これはパスが通っていないことが原因ですので、パスを通す方法を紹介します。

1. 拡張機能「C/C++」をインストール
2. 「File」→「Preferences」→「Settings」をクリック
3. 「includepath」で検索
4. 「C_Cpp > Default: Include Path」の「Edit in settings.json」をクリック
5.  以下のように、```C:\\cygwin64\\usr\\i686-pc-cygwin\\sys-root\\usr\\include\\w32api```を追加する

```json
{
    "terminal.integrated.shell.windows": "C:\\Windows\\System32\\cmd.exe",
    "files.autoGuessEncoding": true,
    "C_Cpp.default.includePath": [
        "C:\\cygwin64\\usr\\i686-pc-cygwin\\sys-root\\usr\\include\\w32api"
    ]
}
```

これでIntelliSenseが有効になり、エラーが表示されなくなったと思います。

ちなみに、```C:\\cygwin64\\usr\\i686-pc-cygwin\\sys-root\\usr\\include\\opengl```に入っている```GL```ファイルはシンボリックリンクであるため、VS Codeで読み込めません。そのためリンク先を指定します。
