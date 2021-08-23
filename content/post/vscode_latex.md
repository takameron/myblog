---
title: "VSCodeでLaTeXの環境を整える"
date: 2020-10-20T22:29:00+09:00
lastmod: 2021-08-23T18:30:01+09:00
author: "ぶっち"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1602317181/Blog-personal/vscode_latex/thumb.png"]
categories: ["Tips"]
tags: []
archives: ["2020", "2020-10"]
toc: true
draft: false
---

パソコンを買い換えるたびにLaTeXの執筆環境の構築をしているので、方法をメモとして残しておきます。
ファイルを保存すると自動でコンパイルが実行されPDFに反映される、我ながら最強の環境です。

この記事では、(u)platex→dvipdfmxの順でPDFを生成する方法を紹介します。

事前にLaTeXのインストールを済ませてください。

## 拡張機能のインストール
{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1629705160/Blog-personal/vscode_latex/plugin-install.png" alt="LaTeX Workshop」をインストール" caption="拡張機能のインストール" >}}

拡張機能の検索欄で「LaTeX Workshop」と検索し、James Yuさんが作成された拡張機能をインストールします。
[マーケットプレイスのページ](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop "LaTeX Workshop - Visual Studio Marketplace")にある「Install」ボタンをクリックしてもインストールできます。

## 自動実行の設定
自動実行の設定は2種類あります。1つ目の「ユーザ設定」はエディタ自体に設定をするものであり、2つ目の「ワークスペース設定」はフォルダごとに設定します。
メリットとデメリットは以下の通りです。

||ユーザー設定|ワークスペース設定|
| :--- | :--- | :--- |
|メリット|1箇所で設定すればすべての執筆物で<br>同じ環境が使える|執筆物ごとに設定ができる|
|デメリット|執筆物ごとの設定ができない<br>（ワークスペース設定として上書きはできる）|執筆物ごとに設定ファイルを置く必要がある|

個人的には、フォルダごとコピーすればどのコンピュータでも環境を再現できるので、ワークスペース設定のほうが好みです。
ユーザー設定は[こちら](#ユーザー設定)、ワークスペース設定は[こちら](#ワークスペース設定) で紹介しています。

### ユーザー設定
{{< info >}}
古い（最近のブログ記事等ではあまり紹介されていない）方法ですが、手っ取り早くたくさんのLaTeXファイルをコンパイルできる方法として紹介します。
{{< /info >}}

ここでは、Windowsで日本語化拡張機能を入れない環境のスクリーンショットを載せながら手順を紹介します。
VSCodeのバージョンや日本語化拡張機能の有無で表示は変わりますが、大体同じ手順だと思います。

まず、「File」→「Preferences」→「Setting」を選択します。
（Macで日本語化拡張機能を入れた状態では「Code」→「基本設定」→「設定」です）
{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1602314515/Blog-personal/vscode_latex/setting1.png"  alt="設定画面を開く" caption="設定画面を開く" >}}

右上にあるファイルのアイコンをクリック。
{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1602315314/Blog-personal/vscode_latex/setting2.png"  alt="設定画面" caption="設定画面" >}}

個人設定用のJSONファイルが開きます。
このファイルに設定を記述すると、現在コンピュータにサインインしているアカウントでVSCodeを使った時に、この設定が反映されます。
{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1602314515/Blog-personal/vscode_latex/setting3.png"  alt="ユーザ設定のJSONファイル" caption="JSONファイルでユーザ設定をする" >}}

このファイルに、以下の内容を上書きします。既存の設定がある場合、最後の```"ほげほげ": "ふがふが"```のような行の最後に```,```をつけ、以下のテキストの一番外側の```{}```の内側を```"ほげほげ": "ふがふが",```の次の行に続けて貼り付けてください。

```JSON
{
    "latex-workshop.latex.recipes": [
        {
            "name": "platex",
            "tools": [
                "platex",
                "pbibtex",
                "platex",
                "platex",
                "dvipdfmx"
            ]
        }
    ],
    "latex-workshop.latex.tools": [
        {
            "name": "platex",
            "command": "platex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-kanji=utf8",
                "-shell-escape",
                "%DOC%"
            ]
        },
        {
            "name": "dvipdfmx",
            "command": "dvipdfmx",
            "args": [
                "%DOCFILE%.dvi"
            ]
        },
        {
            "name": "pbibtex",
            "command": "pbibtex",
            "args": [
                "-kanji=utf8",
                "%DOCFILE%"
            ]
        }
    ]
}
```

この設定は[こちらのサイト](https://www.asrobot.me/entry/2018/12/05/193220/ "VSCodeで日本語TeXの自動コンパイル環境を構築する方法 - ASRobot")から引用いたしました。これはplatexでコンパイルする時の最低限の設定です。platexでコンパイルする際はこの設定で完璧ですが、他のコマンドでコンパイルしたい場合は書き換えたり追記してください。

これでLaTeXファイルを自動コンパイルできるようになりました。

### ワークスペース設定
ここで紹介する全ての設定を実施したものをGitHubにあげました。LaTeX文章を書き始めるテンプレートのようになっています。LaTeX、VSCode、拡張機能をインストールし、あとはこのテンプレートをもとに文章を作成すれば自動コンパイルされます。

{{< blogcard "https://github.com/takameron/vscode-uplatex" "takameron/vscode-uplatex" >}}

以下からZipファイルをダウンロードできます。

{{< download "https://github.com/takameron/vscode-uplatex/archive/refs/heads/main.zip" "VSCode用LaTeXテンプレート" >}}

ファイル構成は以下のようになっています。```.vscode```ディレクトリの中に、インストールを推奨する拡張機能を指定する```extensions.json```、設定を記述する```settings.json```が入っています。```.latexmkrc```ファイルにはLaTeXでのコンパイル方法を記述します。```test.tex```が文書ファイルで、ファイル名は自由です。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1602323919/Blog-personal/vscode_latex/tree.png" img_w=576 img_h=310 w=576 form="landscape" alt="ファイル構成" caption="ファイル構成" >}}

#### インストールを推奨する拡張機能を指定（オプション）
LaTeXの自動コンパイルには「LaTeX Workshop」という拡張機能が必要であり、これまでの手順ですでにインストールしています。
しかし、新しい環境ではまだインストールしていないかもしれません。

ここでは、指定した拡張機能がインストールされていない場合に、インストールするように推奨するメッセージをVSCodeが出せるようにします。
そのため、この設定は必須ではありません。

1. 最初に```.vscode```ディレクトリを作成します。
Windowsではエラーが表示されるかもしれませんが、その場合はフォルダ名を```.vscode.```としてみてください。

2. ```.vscode```ディレクトリの下に```extensions.json```ファイルを作成します。
```extensions.json```ファイルを開いて、以下のテキストを貼り付けてください。

```json
{
    "recommendations": [
      "james-yu.latex-workshop"
    ]
}
```

これで「LaTeX Workshop」がインストールされていない環境でこのフォルダをVSCodeで開くと、「LaTeX Workshop」をインストールするようにメッセージが表示されます。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1602325385/Blog-personal/vscode_latex/recommend.png"  alt="インストール推奨メッセージ" caption="インストールするか尋ねてくる" >}}

#### VSCodeの設定
```.vscode```ディレクトリの下に```settings.json```ファイルをおくと、このワークスペース（フォルダ）内でのみ有効な設定が読み込まれます（ユーザ設定と競合していたらこちらの設定が優先されます）。

コンパイルにはLatexmkを使うため、この設定ファイルにLatexmkを呼び出す設定を記述します。
「LaTeX Workshop」によって、LaTeX文書を保存するとこの設定に従って文章のコンパイルが開始されます。

1. ```.vscode```ディレクトリの下に```settings.json```ファイルを作成します。

2. ```settings.json```ファイルを開いて、以下のテキストを貼り付けてください。

```json
{
    "latex-workshop.latex.recipes":[{
        "name": "uplatex",
        "tools" : [
          "latexmk"
        ]
      }],
      "latex-workshop.latex.tools": [{
        "name": "latexmk",
        "command": "latexmk",
        "args" : [

        ]
      }
    ],
      "latex-workshop.view.pdf.viewer":"tab", // 「Ctrl + Alt + v」で使うPDFビューワをタブに設定
      "latex-workshop.latex.autoClean.run": "onBuilt" // ビルド時に一時ファイル(.auxなど)を削除
}
```

```"latex-workshop.view.pdf.viewer":"tab"```はPDFの開き方を指定する項目で、他には外部アプリやブラウザを指定できます。設定方法はwebでお探しください。

#### LaTeXのコンパイル方法の設定
コンパイルにはLatexmkというツールを使います。
Latexmkとは、「文書を作成するのに必要な回数タイプセットしてくれるツール」[^1]で、少ない行数でコンパイル方法の指定ができます。
[^1]: [Latexmk - TeX Wiki](https://texwiki.texjp.org/?Latexmk "Latexmk - TeX Wiki")

1. ```.latexmk```ファイルを作成します。Windowsではエラーが表示されるかもしれませんが、その場合はフォルダ名を```.latexmk.```としてみてください。

2. ```.latexmk```ファイルを開いて、以下のテキストを貼り付けてください。

```Perl
#!/usr/bin/env perl

$latex            = 'uplatex -shell-escape -kanji=utf8 -synctex=1 -halt-on-error -interaction=nonstopmode -file-line-error %O %S';
$latex_silent     = 'uplatex -shell-escape -kanji=utf8 -synctex=1 -halt-on-error -interaction=batchmode %O %S';
$bibtex           = 'pbibtex %O %S';
$biber            = 'biber --bblencoding=utf8 -u -U --output_safechars';
$dvipdf           = 'dvipdfmx %O -o %D %S';
$makeindex        = 'mendex %O -o %D %S';
$max_repeat       = 5;
$pdf_mode         = 3;
$pvc_view_file_via_temporary = 0;

# clean up
$clean_full_ext = "%R.synctex.gz"
```

今回の設定では、uplatex, dvipdfmxを使ってPDF化しています。

#### コンパイルしてみよう！（動作確認）
これで自動コンパイルの設定が終わりました！
動作を確認してみます。

```test.tex```というファイルを作成し、以下のテキストを貼り付けてください。

```LaTeX
\documentclass[a4j,uplatex]{jsarticle}

\usepackage[dvipdfmx]{graphicx} % 画像読み込み
\usepackage[dvipdfmx]{color} % カラー出力（色指定ができる）
\usepackage[hidelinks,bookmarksnumbered=true,dvipdfmx]{hyperref} % PDFのメタデータ埋め込み
\usepackage{pxjahyper} % しおり・タイトル等の日本語の文字化け防止
\usepackage{here} % 図表の位置を強制的に指定
\usepackage{url} % URIをそのまま表示＆ハイパーリンク化

% PDFのメタデータ設定
% \hypersetup{
%   pdftitle={テスト}, %タイトル
%   pdfauthor={著者}, %著者
%   pdfsubject={VSCode環境におけるLaTeXファイルの扱いに関する研究}, %件名
%   pdfkeywords={Visual Studio Code; LaTeX;} %キーワード
% }

\begin{document}

\section{はじめに}

吾輩は猫である。名前はまだ無い。 

式\ref{eq:1}はオイラーの等式である。

\begin{equation}
  \label{eq:1}
  \mathrm{e}^{\mathrm{i}\pi} + 1 = 0
\end{equation}

% 画像読み込み
% \begin{figure}[H]
%     \centering
%     \includegraphics[height=4cm]{image/1.pdf}
%     \caption{画像}
%     \label{fig:1}
% \end{figure}

ほげほげ\cite{refer1}ふがふが\cite{refer2}。

% 参考文献
\begin{thebibliography}{9}
  \bibitem{refer1} 著者1, 『タイトル1』, 出版社, 出版年, pp.000-111
  \bibitem{refer2} 著者2, \url{https://www.takameron.info}, 2020年10月10日閲覧
\end{thebibliography}

\end{document}
```

ファイルを保存すると、自動でコンパイルが開始され、PDFファイルが生成されるはずです。
PDFファイルの開き方は、以下の通りです。

1. PDFファイルをダブルクリックして「このまま開きますか？」をクリック
2. LaTeXファイルを開いている時に「Ctrl + Alt + v」（Macなら「option + command + v」）を同時押し

PDFファイルを開いておけば、LaTeXファイルを保存すると自動でコンパイルが開始されPDFが更新されます。

以上です。お疲れ様でした！

## 【おまけ】web表示用に最適化
QPDFというコマンドを使うと、PDFをweb表示用に最適化できます。PDFの内部構造を変更するだけであり、画質が落ちるなどデメリットが特にあるわけではないので、最適化しておくと良いと思います（しなくてもあまり問題ありませんが）。

ここでは、自動でqpdfコマンドを実行し、web表示用に最適化する方法を紹介します。

まず、QPDFというコマンドがインストールされている必要があります。LaTeXのインストール時にWindowsでは標準でインストールされ、MacやLinuxではインストールされないようです（詳しく確かめていないのでわかりません）。ターミナルで```qpdf --version```と入力して実行すると、インストールされているかを確認できます。
インストールされていない場合、インストール方法はここでは紹介しませんのでwebでお探しください。

qpdfコマンドがインストールされていることを確認できたら、```.vscode/settings.json```を以下のテキストに置き換えます。

```json
{
    "latex-workshop.latex.recipes":[{
        "name": "uplatex",
        "tools" : [
          "latexmk",
          "web_optimisation"
        ]
      }],
      "latex-workshop.latex.tools": [{
        "name": "latexmk",
        "command": "latexmk",
        "args" : [

        ]
      },{
        "name": "web_optimisation",
        "command": "qpdf",
        "args" : [
          "--linearize",
          "%DOCFILE%.pdf",
          "web.pdf"
        ]
      }
    ],
      "latex-workshop.view.pdf.viewer":"tab", // 「Ctrl + Alt + v」で使うPDFビューワをタブに設定
      "latex-workshop.latex.autoClean.run": "onBuilt" // ビルド時に一時ファイル(.auxなど)を削除
}
```

"latex-workshop.latex.recipes"の"tools"に```"web_optimisation"```を追加し、"latex-workshop.latex.tools"に```"web_optimisation"```の設定を追加しました。
これで、元々生成されていたPDFファイルに加えて、```web.pdf```ファイルが生成されます。

実際にWeb表示用に最適化されているか、確認します。

まずはVSCodeでPDFファイルを開きます。PDFの上部にカーソルを持っていきメニューバーを表示させ、「>>」というアイコンをクリックし、「文章のプロパティ...」を選択します。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1602322173/Blog-personal/vscode_latex/pdf_property1.png"  alt="PDFのプロパティを開く" caption="PDFのプロパティを開く" >}}

「Web表示用に最適化」の項目を確認し、「はい」になっていれば最適化されています（「いいえ」の場合は最適化されていません）。

{{< cloudinary src="https://res.cloudinary.com/tsukayaku/image/upload/v1602322173/Blog-personal/vscode_latex/pdf_property2.png"  alt="PDFのプロパティ" caption="「Web表示用に最適化」を確認" >}}