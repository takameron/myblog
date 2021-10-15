---
title: "MacでInkscapeをビルドする"
date: 2021-10-16T07:49:49+09:00
lastmod: 2021-10-16T07:49:49+09:00
author: "ぶっち"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1632986420/Blog-personal/inkscape_build_on_mac/thumbnail.png"]
categories: ["ソフトウェア・サービス"]
tags: []
archives: ["2021","2021-10"]
toc: false
draft: false
---

HomebrewをインストールしているMacで、Inkscapeをソースコードからビルドしてみました。
[こちらの公式Wiki](https://wiki.inkscape.org/wiki/index.php?title=CompilingMacOsX "CompilingMacOsX - Inkscape Wiki")通りにやってもパスの関係で失敗しましたので、忘備録として残しておきます。

実行環境は以下の通りです。
| | バージョン |
| --- | --- |
| パソコン | MacBook Pro (13-inch, 2020, Four Thunderbolt 3 ports) |
| OS | macOS Big Sur 11.6 |
| Inkscape | Inkscape 1.2-dev (942b66973d, 2021-09-28) |

まずは公式Wikiと同様にパッケージをインストールします。

```shell {linenos=false}
brew install \
    adwaita-icon-theme \
    bdw-gc \
    boost \
    cairomm \
    ccache \
    cmake \
    double-conversion \
    gettext \
    gsl \
    gspell \
    gtk-mac-integration \
    gtkmm3 \
    imagemagick \
    intltool \
    lcms2 \
    libomp \
    libsoup \
    libxslt \
    ninja \
    poppler \
    potrace
```

次に、任意のディレクトリに移動し、**このまま**コマンドを実行します。

全体的に規模が大きいので、1時間以上はかかるかもしれません。

私はGitでクローンしてきたらそのディレクトリに入ってコマンドを実行していたので、場所が違うと気がつくのに時間がかかりました。

```shell {linenos=false}
git clone --recurse-submodules https://gitlab.com/inkscape/inkscape.git

LIBPREFIX="/opt/local"

# where to install
PREFIX="$PWD/install-prefix"
# to load icu library
export CMAKE_PREFIX_PATH=/usr/local/opt/icu4c
# to load libgsl(when ninja install)
export LIBRARY_PATH=/usr/local/lib

# where to build
mkdir build
cd build

cmake \
    -G Ninja \
    -DCMAKE_PREFIX_PATH="$LIBPREFIX" \
    -DCMAKE_INSTALL_PREFIX="$PREFIX" \
    -DCMAKE_C_COMPILER_LAUNCHER=ccache \
    -DCMAKE_CXX_COMPILER_LAUNCHER=ccache \
    -DWITH_OPENMP=OFF \
    -DIntl_INCLUDE_DIR="$LIBPREFIX/opt/gettext/include" \
    ../inkscape

ninja
ninja install
```

ビルドが終わると```install-prefix```というディレクトリが作成されています。
```install-prefix/bin/inkscape```が実行ファイルです。
