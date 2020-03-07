# Python ハンズオン

[![Python version](https://img.shields.io/badge/Python-3.8-blue.svg?style=for-the-badge)](https://docs.python.org/3/)
[![MIT License](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](LICENSE)

## 目的

- 基礎的な Python 開発能力の取得
- 良いコードを書く練習
- Git, GitHub が使えるようになる

## 形式

演習形式で行う。
この講習で開発したコードは GitHub に上げて，プルリクエストを送る形で提出する。(Git, GitHub の使い方については最初の講習で説明する)

## 課題に取り組むにあたって

- 積極的に先輩に質問したり，同期と相談しながら取り組むこと
- わからないのは問題ないが，どうしてわからないのか，どこにつまづいているのか言語化出来るようにすること
- ググる，コピペなんでも OK
  - ググる力 (googlability) も能力の一つ
  - ただし，どうしてそのコードを書いたのかきちんと言語化出来るように

> 参考：[Python 公式ドキュメント](https://docs.python.org/ja/3/)

## 環境構築

- 実行環境：OSX (macOS)

### 1. Homebrew のインストール

ターミナルを起動して以下のコマンドを実行

```bash
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

#### `Homebrew` とは？

OSX (macOS) 用のパッケージマネージャー。
様々なパッケージの管理 (インストール，アップグレード，etc.) を容易に行うことが出来るコマンドラインツール。

- プログラム言語 (Python, Go, Node.js など)
- テキストエディタ (Vim, Neovim, Emacs など)
- コマンドラインツール (git, curl, tree など)

> 参考：[Homebrew 公式サイト](https://brew.sh/index_ja)

### 2. pyenv のインストール

`Homebrew` を用いて `pyenv` をインストール

```bash
$ brew install pyenv
```

`pyenv` を使用するためのセットアップを行う

```bash
$ echo 'export PYENV_ROOT=/usr/local/var/pyenv' >> ~/.bash_profile
$ echo 'eval "$(pyenv init -)"' >> ~/.bash_profile
$ source ~/.bash_profile
```

`pyenv` を用いて，Python の最新バージョン (3.8.2) をインストール，およびセットアップを行う

```bash
$ pyenv install 3.8.2
$ pyenv global 3.8.2
$ pyenv rehash
```

#### `pyenv` とは

Linux において，Python の実行環境を管理するためのツール。
2.x 系, 3.x 系を使い分ける，開発プロジェクトごとにバージョンを切り替えることなどに用いられる。

> 参考：[pyenv とは](https://qiita.com/mogom625/items/b1b673f530a05ec6b423)

### 3. Pipenv のインストール

`Homebrew` を用いて `Pipenv` をインストール

```bash
$ brew install pipenv
```

`Pipenv` の設定を環境変数を用いて行う

```bash
# プロジェクト直下に仮想環境を構築する
echo 'export PIPENV_VENV_IN_PROJECT=1' >> ~/.bash_profile
# デフォルトで用いる Python を指定
echo 'export PIPENV_PYTHON="$PYENV_ROOT/shims/python"' >> ~/.bash_profile

source ~/.bash_profile
```

#### `Pipenv` とは

Python での依存関係の管理やパッケージ化を行うためのツール。
`Pipfile` に対してパッケージの追加および削除を行うのに加え，プロジェクト用の仮想環境を作成し，管理する。
また `Pipfile.lock` も同時に生成し，これを利用して常にビルドが同じ結果になるようにする。

> 参考：[Pipenv 公式ドキュメント](https://pipenv-ja.readthedocs.io/)

### なぜ `Pipenv` を用いるのか？

仮想環境を使わない場合、2. でインストールした Python に対して、`Pip` でパッケージをインストールすることになる。
`Pip` は `pyenv` で Python をインストールした際に付属している。
`Pip` は Python パッケージをインストールした Python の直下にインストールするツール、`Pipenv` は仮想環境下にインストールするツールと覚えておけば良い。

`Pip` の場合、環境構築が簡単な反面、何らかの理由で環境が壊れてしまった場合、Python ごとアンインストールする必要が出てくるかもしれない。
また、同じバージョンの Python で、異なるバージョンの Python パッケージを複数プロジェクトで使い分けるといったことができない。

その点、`Pipenv` を使った環境では、何か起きたら仮想環境の削除 → 再作成を気軽に行うことができる。
また、各仮想環境は完全に独立しているので、「あるプロジェクトで起きた不具合が他に波及する」、といったことがなく安全だ。
特段の理由がない限り、`Pipenv` で管理しておくのが良いだろう。

#### `Pip` とは

Python のパッケージを管理するためのツール。
サードパティ (公式が配布していないパッケージ) を管理するのに用いる。

> 参考：[[Python 入門] pip とは？ 使い方をわかりやすく解説](https://www.sejuku.net/blog/50417)

## テキストエディタ

テキストエディタとは，PC 上でメモやプログラムを書くことの出来るソフト。
Windows では「メモ帳」，Mac では「テキストエディット」という名前のアプリケーションがデフォルトで入っている。

メモ帳等でもプログラミングをすることは出来るが，プログラミング用のテキストエディタを使うことで効率よく開発作業が行うことが出来る。

様々なテキストエディタがあるがどれを使っても問題ないので，好みで選ぶと良い。

### おすすめ

#### Visual Studio Code (VSCode)

Microsoft が開発したオープンソースのテキストエディタ。
高機能かつインターフェースが洗練されているため，非常に使いやすい。
正直これが一番良いと思う。

> 公式 HP：https://code.visualstudio.com/

#### Atom

GitHub が公開したテキストエディタ。
便利なプラグインが多く，またインターフェースが非常に見やすいため，初心者でも使いやすい。
Windows，macOS，Linux で利用できるので誰でも手軽に使える。
ただ少し動作が重たい。

> 公式 HP：https://atom.io/

#### Vim

主に CUI 環境 (ターミナル) で使われるエディタ。
歴史が古く多くのユーザーに使われている。
独特のキーバインドは最初はとっつきづらいが，なれると高速で作業ができるようになる。

> 公式 HP：https://www.vim.org/

#### Emacs

Vim 同様 CUI 環境で使われるエディタ。
ターミナル上でのキーバインドと親和性が高く，最初は Vim よりは使いやすい？かもしれない。

> 公式 HP：https://www.gnu.org/software/emacs/
