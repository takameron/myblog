---
title: "dotfilesを作ってMacを簡単セットアップ"
date: 2021-11-02T14:17:00+09:00
lastmod: 2021-11-02T14:17:00+09:00
author: "ぶっち"
images: ["https://res.cloudinary.com/tsukayaku/image/upload/v1580351945/Blog-personal/thumbnail/programming.jpg"]
categories: ["Tips"]
tags: []
archives: ["2021", "2021-11"]
toc: true
draft: false
---

簡単な手順で、自分の使い慣れた環境をセットアップする方法を紹介します。

シェルスクリプトになっているので、このスクリプトを動かすために何かをインストールする必要はありません。
必要最小限の事前準備で済みます。

こちらにリポジトリがありますので、ぜひご自由にご利用ください。
（CC0でライセンスされているため改変や再配布は自由ですが、利用に関して損害を被った場合の責任は負いませんのでご注意ください。）

{{< blogcard "https://github.com/takameron/dotfiles-mac" "takameron/dotfiles-mac: Dotfiles for Mac" >}}

## 構成
ファイル構成は以下のようになっています。

セットアップする項目ごとにディレクトリがあります。
```install.sh```はセットアップを行うコマンドを記述したシェルスクリプトです。
その他はセットアップに必要なファイルであり、いろいろなソフトウェア向けの設定ファイルや、インストールするソフトウェアの一覧などがあります。

一番上のディレクトリにある```install.sh```が、各ディレクトリにある```install.sh```を順に実行しています。

```text {linenos=false}
.
├── 1_homebrew
│   ├── Brewfile
│   └── install.sh
├── 2_asdf
│   ├── .default-gems
│   ├── .default-npm-packages
│   └── install.sh
├── 3_macos
│   └── install.sh
├── 4_dotfiles
│   ├── .gitconfig
│   ├── .gitignore
│   ├── .plugins.zsh
│   ├── .vimrc
│   └── install.sh
├── 5_vscode
│   ├── install.sh
│   └── setting.json
└── install.sh
```

## 手順

### 順にセットアップしていくスクリプト
最初に、各ディレクトリ内の```install.sh```を実行していくスクリプトを紹介します。

まず、このスクリプトが存在するディレクトリにおいて、ディレクトリ一覧を取得します。
これを```sort```コマンドで昇順にすることで、たどっていくディレクトリの順番を変えられます。
あとは、for文で各ディレクトリ内の```install.sh```を順に実行するだけです。

```shell
#!/bin/sh

dirs=$(find "$PWD" -depth 1 -type d -not -name '.*' | sort -n)
for dir in $dirs;
do
  echo 📁 "$dir"
  sh "$dir"/install.sh
done
```

### Homebrew
次は、Mac向けのパッケージ管理システムであるHomebrew関連の処理です。

ここで紹介するスクリプトでは、以下の処理を行っています。

* Homebrewのインストール
* ディレクトリの権限設定
* ```Brewfile```に記載されたソフトウェアのインストール
* パスの設定

```! (type brew > /dev/null 2>&1)```の箇所では、```brew```コマンドが存在するか否かを判定しています。
```type```コマンドは、引数に与えられたコマンドのパスを表示します。
また、コマンドが見つかれば戻り値0、見つからなければそれ以外を返します。
この動作を利用すると、コマンドが使えるか否かの判定ができます。
```2>&1```でエラー出力(2)を標準出力(1)にリダイレクトし、なおかつ```/dev/null```にリダイレクトすることで、```type```コマンドが表示する文字列は虚無に消え、戻り値だけを利用できます。

パスの設定については、インストールするソフトウェアごとに適切なパスを設定してください。

また、たまにパスワードの入力を要求してくる場合があります。
放置して終わった頃を見計らって戻ってきたらパスワード入力の要求で止まっていた、ということもあり得るので、シェルスクリプトを改良するか、たまに様子を確認してください。

```
#!/bin/sh

# brewコマンドがなければインストール
if ! (type brew > /dev/null 2>&1); then
  xcode-select --install
  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
fi

# 権限設定
sudo chown -R "$(whoami)":admin /usr/local/*
sudo chmod -R g+w /usr/local/*

# Brewfileを実行
cd "$PWD"/homebrew || exit
brew bundle
cd - || exit

# パスの設定
s_path=""
s_manpath=""

# coreutils
s_path="/usr/local/opt/coreutils/libexec/gnubin:${s_path}"
s_manpath="/usr/local/opt/coreutils/libexec/gnuman:${s_manpath}"

# curl
s_path="/usr/local/opt/curl/bin:${s_path}"

echo "export PATH=\"${s_path}"'$PATH"' >> ~/.zshrc
echo "export MANPATH=\"${s_manpath}"'$MANPATH"' >> ~/.zshrc
. ~/.zshrc

echo "👍 Homebrew setting is done!"
```

```Brewfile```はこんな内容です。

ソフトウェアは3種類に分かれています。
```brew```コマンドが使える状況でしたら、```brew search [パッケージ名]```で調べた時に、「Formulae」になっていれば```brew "[パッケージ名]"```、「Casks」になっていれば```cask "[パッケージ名]"```です。

App Storeからインストールしたものは```mas "[パッケージ名]",  id: [ID]```になります。
IDは、```mas```コマンドをインストールしていれば、```mas list```や```mas search [パッケージ名]```で調べられます。

```text
tap "homebrew/cask-versions"
tap "homebrew/cask-drivers"

brew "coreutils"
brew "curl"
brew "wget"
brew "git"
brew "tree"
brew "gpg"
brew "pinentry-mac"
brew "gnu-tar"
brew "pixz"
brew "gnuplot"

cask "adguard"
cask "adobe-acrobat-reader"
cask "arduino"
cask "authy"
cask "blackhole-16ch"
cask "clip-studio-paint"
cask "coteditor"
cask "cryptomator"
cask "cyberduck"
cask "docker"

mas "Bitwarden", id: 1352778147
mas "Keepa - Price Tracker", id: 1533805339
mas "Microsoft OneNote", id: 784801555
mas "Microsoft To Do",id: 1274495053
mas "Mia Translate", id: 1500605326
mas "Keynote", id: 409183694
mas "Numbers", id: 409203825
mas "Pages", id: 409201541
mas "Telephone", id: 406825478
mas "Vectornator: Design Software", id: 1219074514
```

### asdf
私は各種実行環境をasdfで管理しているので、asdfで環境構築する方法を紹介します。

スクリプトでは、以下の処理を行っています。

* asdfをインストール
* シェルの起動時にスクリプトを読み込むように設定
* ```default-*```ファイルのシンボリックリンクを貼る
* プラグイン・各開発環境の最新版をインストール

```shell
#!/bin/sh

# asdfコマンドがなければasdfをインストール
if ! (type asdf > /dev/null 2>&1); then
  if ! (type brew > /dev/null 2>&1); then
    sh homebrew/install.sh
  fi
  brew install coreutils curl git
  brew install asdf
fi

# add to shell
echo ". $(brew --prefix asdf)/asdf.sh" >> ~/.zshrc

# Default Packages
basename -a "$PWD"/asdf/.default-* | xargs -I{} ln -sfv "$PWD"/asdf/{} ~/{}

# === asdf-nodejs ===
# Requirements
brew install coreutils gpg gawk
# Install plugin
asdf plugin-add nodejs https://github.com/asdf-vm/asdf-nodejs.git
# Import the Node.js release team's OpenPGP keys to main keyring
bash -c '${ASDF_DATA_DIR:=$HOME/.asdf}/plugins/nodejs/bin/import-release-team-keyring'
# Install Node.js
asdf install nodejs latest
asdf global nodejs "$(asdf list nodejs | tail -1 | sed -e 's/ //g')"

# === asdf-python ===
# Install plugin
asdf plugin-add python https://github.com/danhper/asdf-python
# Install Python
asdf install python latest
asdf global python "$(asdf list python | tail -1 | sed -e 's/ //g')"

# === asdf-ruby ===
# Requirements(optional, but recommended)
brew install openssl readline
echo "export RUBY_CONFIGURE_OPTS=\"--with-openssl-dir=\"$(brew --prefix openssl@1.1)\"\"" >> ~/.zshrc
# Install plugin
asdf plugin-add ruby https://github.com/asdf-vm/asdf-ruby.git
# Install Ruby
asdf install ruby latest
asdf global ruby "$(asdf list ruby | tail -1 | sed -e 's/ //g')"

echo "👍 asdf install is done!"
```

### Macの設定
Mac内において各種設定の一部は、```.plist```という拡張子を持つplistファイル（プロパティリスト）に保存されます。
```defaults```コマンドを使うと、読み込み可能なplistファイルにある設定値の読み書きができます。

というわけで、ここでは```defaults```コマンドを使ってMacの各種設定をします。

ちなみに、設定値は公式に公開されているものではなく、ネット上で先人たちが見つけたものです。
また、Macのバージョンによってもいろいろな変更点があるようです。
私が試した範囲では、設定値を見つけられなかったり、ネット上の情報を頼りに設定しても反映されないことが多々ありました。
なので、運が良ければ設定できる、程度の受け止めのほうが良いかもしれません。

ちなみに設定値の見つけ方は、なんらかの設定の変更前後で```defaults read > [ファイル名]```を実行して設定値一覧を書き出し、```diff```コマンドで差分を見ると見つけやすいと思います。

以下のシェルスクリプトは一例です。
ここに載っているコマンドには有効でないものも含まれています。

```shell
#!/bin/sh

# --- Finder ---
# 隠しファイルを表示
defaults write com.apple.finder AppleShowAllFiles -bool true
# すべての拡張子のファイルを表示
defaults write NSGlobalDomain AppleShowAllExtensions -bool true
# ステータスバーを表示
defaults write com.apple.finder ShowStatusBar -bool true
# パスバーを表示
defaults write com.apple.finder ShowPathbar -bool true
# ドライブをデスクトップに表示
defaults write com.apple.finder ShowHardDrivesOnDesktop -bool true
defaults write com.apple.finder ShowExternalHardDrivesOnDesktop -bool true
defaults write com.apple.finder ShowRemovableMediaOnDesktop -bool true
defaults write com.apple.finder ShowMountedServersOnDesktop -bool true
killall Finder

# ネットワークストレージに .DS_Store ファイルを作成しない
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true
# USBメモリに .DS_Store ファイルを作成しない
defaults write com.apple.desktopservices DSDontWriteUSBStores -bool true

# --- Security ---
# ファイアーウォールをオン
sudo defaults write /Library/Preferences/com.apple.alf globalstate -int 1

# --- Dock ---
# “自動的に非表示”をオン
defaults write com.apple.dock autohide -bool true
# 最近使ったアプリケーションを非表示
defaults write com.apple.dock show-recents -bool false
killall Dock

# --- SystemUIServer関係 ---
# 時計で日付を表示（例：9月20日(木) 23:00）
defaults write com.apple.menuextra.clock DateFormat -string 'EEE MMM d HH:mm:ss'
# バッテリーの割合（%）を表示
defaults write com.apple.menuextra.battery ShowPercent -string "YES"
# スクリーンショットのドロップシャドウを付けない
defaults write com.apple.screencapture disable-shadow -bool true
killall SystemUIServer

# --- Safari ---
# アドレスバーに完全な URL を表示
defaults write com.apple.Safari ShowFullURLInSmartSearchField -bool true
# ファイルのダウンロード後に自動でファイルを開くのを無効化
defaults write com.apple.Safari AutoOpenSafeDownloads -bool false
# メニューバーに「開発」を表示
defaults write com.apple.Safari IncludeDevelopMenu -bool true
# デバッグメニューをオン
defaults write com.apple.Safari IncludeInternalDebugMenu -bool true
# ステータスバーを表示
defaults write com.apple.Safari ShowStatusBar -bool true
killall Safari

# ---　TextEdit　---
# リッチテキストから標準テキストに変更
defaults write com.apple.TextEdit RichText -int 0

echo "👍 MacOS setting is done!"
```

### dotfiles
いろいろなソフトウェアは、設定情報をファイルを書き出していることがあります。
ドット（.）から始まるこれらのファイルを、ドットファイルと呼ぶことがあります。

このシェルスクリプトでは、以下の処理を行っています。

* ドット（.）から始まるファイルのシンボリックリンクをホームディレクトリに貼る
* Zinit（Zsh用のプラグインマネージャ）をインストール
* ```.DS_Store```ファイルを削除するコマンドを追加

正直```.DS_Store```ファイルって邪魔ですよね〜。
USBメモリを介してファイルを渡したり、ディレクトリごと何かしらの方法で渡したりするとき、Windowsユーザに何か意味のあるファイルだと思われると、説明しないといけません。
というわけで、現在いるディレクトリの配下の再帰的に探して```.DS_Store```ファイルを削除するコマンドを追加しています。

```shell
#!/bin/sh

# link
basename -a "$PWD"/dotfiles/.??* | xargs -I{} ln -sfv "$PWD"/dotfiles/{} ~/{}

# Zinit (Zsh plugin manager)
sh -c "$(curl -fsSL https://raw.githubusercontent.com/zdharma/zinit/master/doc/install.sh)"
echo "source ~/.plugins.zsh" >> ~/.zshrc

# Delete .DS_Store
echo "alias dsstore=\"find . -name '*.DS_Store' -type f -ls -delete\"" >> ~/.zshrc

echo "👍 dotfiles link is done!"
```

### VS Codeの設定
最後に、Visual Studio Codoの設定をします。

このシェルスクリプトでは、以下の処理を行っています。

* VS Codeのインストール
* ```settings.json```のシンボリックリンクを貼る
* 拡張機能のインストール

```shell
#!/usr/bin/env bash

# codeコマンドがなければVSCodeをインストール
if ! (type code > /dev/null 2>&1); then
  if ! (type brew > /dev/null 2>&1); then
    sh homebrew/install.sh
  fi
  brew install --cask visual-studio-code
fi

# settings.jsonの設置
ln -sfv "$PWD"/vscode/settings.json ~/Library/Application\ Support/Code/User/

# プラグインのインストール
pkglist=(
  ms-ceintl.vscode-language-pack-ja # Japanese Language Pack for Visual Studio Code
  ms-vscode-remote.remote-ssh-edit # Remote - SSH: Editing Configuration Files
  ics.japanese-proofreading # テキスト校正くん
  james-yu.latex-workshop # LaTeX Workshop
  wakatime.vscode-wakatime # WakaTime
  editorconfig.editorconfig # EditorConfig for VS Code
  ms-azuretools.vscode-docker # Docker
  ms-vscode.cpptools # C/C++
)

for i in "${pkglist[@]}"; do
  code --install-extension "$i"
done

echo "👍 VSCode setting is done!"
```

```settings.json```はこんな内容にしています。

最近はVS Codeに設定の同期機能があるみたいですが、設定ファイルを作っておけば安心ですし、シェルスクリプトとの相性も良いので私はこの方法で管理しています。

```json
{
    "editor.fontSize": 13,
    "editor.wordWrap": "on",
    "files.autoGuessEncoding": true
}
```

## まとめ
これで説明は以上です。
詳しくは[リポジトリ](https://github.com/takameron/dotfiles-mac "takameron/dotfiles-mac: Dotfiles for Mac")をご覧ください。

シェルスクリプトの実行一発でセットアップが進むのは快適です。
秘伝のタレと化した設定や、インストールしているソフトウェアなどを初期状態のパソコンに入れると、キレイかつ使いやすいという、最善の状態になります。

ぜひ、未来のパソコンセットアップ時を見据え、セットアップ用のシェルスクリプトを作っておくのはいかがでしょうか。
