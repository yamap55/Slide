# Pythonの環境を作るときに気を付けること
## アジェンダ

- はじめに
- 気を付けること一覧
- 1つずつ説明
- RuffとRye、Dev Container
- まとめ

## はじめに

- Pythonの開発環境を作るのは大変。
- 気にすることが多い
- 伝えたいこと
  - Ruff、Rye、Dev Containerを使おう

## 気を付けたいこと一覧

- Pythonのバージョン
- 依存ライブラリ管理
- linter
- コードフォーマッター
- 型チェッカー
- ユニットテスト
- importのソート

1つ1つ見ていきます

## Pythonのバージョン
- 複数のプロジェクトをを扱う場合、Pythonのバージョンが異なることが多い
- 環境をホストPCに作成する場合、異なるバージョンをどのように管理するか。

### 普通にやる場合
Linuxだと以下のようになる

```
$ ls -l /usr/local/bin/python*
lrwxrwxrwx 1 root root     7 May 14 16:26 /usr/local/bin/python -> python3
lrwxrwxrwx 1 root root    10 May 14 16:26 /usr/local/bin/python3 -> python3.12
-rwxr-xr-x 1 root root 18208 May 14 16:26 /usr/local/bin/python3.11
-rwxr-xr-x 1 root root 18208 May 14 16:26 /usr/local/bin/python3.12
```

それぞれインストールされていて、pythonコマンドをpython3にリンクさせて、python3をpython3.12にリンクしている。
バージョンを変更するためにはpython3をpython3.11にリンクさせればよい。

PATH書き換えるのも良いかもしれない

※環境によってはpythonコマンドはOS等で使われていたりするのでバージョン変更すると良くない
（昔はpythonがpython2を指していたりしてたので大変だったけど、今は下位互換性あるし大丈夫なのか？）

### pyenv

ちょっと前までは一択。今でもたぶん一番使われているのではないか。
簡単シンプルでPythonのバージョンを変更可能。
https://github.com/pyenv/pyenv

### Dev Container

切り替えが手間なら環境ごと作ればよいじゃない。
https://code.visualstudio.com/docs/devcontainers/containers

`FROM python:3.12` とすれば3.12, `FROM python:3.11` とすれば 3.11。簡単だね。

## 依存ライブラリ管理

標準モジュールのみの開発はほぼなく、外部ライブラリが必須

### pip
- Python自体の標準機能は `pip`
  - https://peps.python.org/pep-0453/
- 設定ファイルは `requirements.txt`（実は名前は何でもよい）

```bash
# 特定のライブラリをインストール
pip install requests
# 設定ファイルを元にライブラリをインストール
pip install -r requirements.txt
```

### pipの問題点その1

- 依存ライブラリの依存ライブラリのバージョンを管理することができない

### 具体例
- アプリケーションが「libA」と「libB」を使用している。
- 「libA」は「libX」<2.0に依存している
- 「libB」は「libX」>1.0に依存している

※ここで大事なのはアプリケーション開発者は「libX」について気にかけていないということ

- アプリケーションの `requirements.txt`
```config
libA==1.0
libB==2.0
```

- 「libA」の `requirements.txt`

```config
libX<2.0
```

- 「libB」の `requirements.txt`

```config
libX>=1.0
```

### libXの最新版が1.5であった場合

`pip install -r requirements.txt`

```
$ pip freeze
libA==1.0
libB==2.0
libX==1.5
```


### libXの最新版が2.0であった場合

`pip install -r requirements.txt`

```
ERROR: Could not find a version that satisfies the requirement libX<2.0 (from libA) (from versions: 1.0, 1.5, 2.0)
ERROR: No matching distribution found for libX<2.0 (from libA)
```

競合を解決できない。

### どうすれば？

- アプリケーションの `requirements.txt` に競合しない `libX` のバージョンを追加する

```config
libA==1.0
libB==2.0
libX==1.5
```

※手動で。  
※アプリケーションはlibXを使用しないのに。。。

### pipの問題点その2

- 依存ライブラリはグローバルに配置される

インストールされるとpython配下のsite-packagesに格納される。
`/usr/local/lib/python3.12/site-packages/`

つまり、違うプロジェクトであっても同じPythonバージョンを使用すると依存ライブラリは共有される

※ `--user` オプションで `~/.local` 配下にインストールすることもできる

### 具体例

app1とapp2全然異なるアプリケーションを作成しているが、それぞれ異なるバージョンのlibAに依存している

- `~/app1/requirements.txt`

```config
libA==1.0
```

- `~/app2/requirements.txt`

```config
libA==2.0
```

- app1開発時に依存ライブラリをインストール
  - `pip install -r ~/app1/requirements.txt`
- app2開発時に依存ライブラリをインストール
  - `pip install -r ~/app2/requirements.txt`
- app1を再度開発
  - libAのバージョンが2.0に更新されてしまい、app1が動作しない！

### どうすれば？

仮想環境を利用する
https://docs.python.org/ja/3/library/venv.html

```
# app1の仮想環境を作成
python -m venv ~/app2/.venv
source ~/app1/.venv/bin/activate
pip install -r ~/app1/requirements.txt

# app2の仮想環境を作成
python -m venv ~/app2/.venv
source ~/app2/.venv/bin/activate
pip install -r ~/app2/requirements.txt
```

依存ライブラリは仮想環境内に保存されるため別のアプリケーションには影響しない

※activate面倒だし、忘れがち

### poetry
とりあえずpipは問題が多すぎるので現在はpoetryが良く使われている
https://python-poetry.org/

- 競合はpipenv
  - https://pipenv.pypa.io/en/latest/
  - ※poetryが出てくるまでは一択だった気がする
- データアナリスト界隈ではanaconda
  - https://www.anaconda.com/
  - ※商用利用は会社規模によって有料（200名以上）

依存ライブラリの解決、lockファイル作成、仮想環境管理、パッケージングを行える

※pipenvとの違いは早さ（今は変わらないらしい）とパッケージング

## linter

コードから文法エラー、コーディングスタイル、潜在的な脆弱性を検出する
基本的にはpep8という公式のコーディング規約を元にチェックする
https://peps.python.org/pep-0008/

- flake8
  - https://github.com/PyCQA/flake8
- pylint
  - https://github.com/pylint-dev/pylint
- pycodestyle（元pep8）
  - https://github.com/PyCQA/pycodestyle

今はflake8一択

### linterの拡張

- フレームワーク独自コードスタイル
  - https://github.com/rocioar/flake8-django
- pep8よりも厳密なコードスタイル
  - https://github.com/zheller/flake8-quotes/
- 変数、関数の命名ルール
  - https://github.com/PyCQA/pep8-naming
- docstringの制御
  - https://github.com/PyCQA/pydocstyle
- バグや設計上の問題
  - https://github.com/PyCQA/flake8-bugbear
  - http://yamap55.github.io/Slide/index.html?slide=20210806/slide.md
  - 一押し: [昔書いたサンプル](https://github.com/yamap55/flake8-bugbear-sample/tree/master/sample)

※種類が無限にある

## コードフォーマッター

コードスタイルについてチェック、修正する

- black
  - https://github.com/psf/black
- autopep8
  - https://github.com/hhatto/autopep8
  - 日本人作
- yapf
  - https://github.com/google/yapf
  - Google

今はblack一択

### black

基本的には設定なし。blackが正しいと言っているものは正しい。blackに合わせろ。

※クォートを `'` に変更することすらできなかった（今もチェックしないというオプションしかない [Issueは必見](https://github.com/psf/black/issues/118)）

## 型チェッカー

最近のトレンドは型。Pythonも最近のアップデートでは型に力を入れている（3.5から）

- mypy
  - https://github.com/python/mypy
  - Python純正
- Pyright
  - https://github.com/microsoft/pyright
  - Microsoft
- Pylance
  - Python用言語サーバ、Pyright準拠
  - VS Code用拡張機能と思ってOK
- pyre
  - https://github.com/facebook/pyre-check
  - Facebook

mypyが一歩有利？個人的にはPyrightが好き

## ユニットテスト

Pythonの標準はunittest
https://docs.python.org/ja/3/library/unittest.html

とりあえずpytest入れとけ。っという感じ
https://github.com/pytest-dev/pytest

細かいところに手が届く。

エラー時の表示、fixture（モックとか）、パラメーター化、構造化とかとか

## importのソート

importの順番制御
isort一択

## 色々多くない？

Ruff, ryeなら簡単に解決。

ここからは次回。
