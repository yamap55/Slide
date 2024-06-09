Pythonの環境を作るときに気を付けること

- Pythonのバージョン
- 依存ライブラリ管理
- linter
- コードフォーマッター
- 型チェッカー
- ユニットテスト
- importのソート


1つ1つ考える


## Pythonのバージョン
複数のProjectを扱う場合、Pythonのバージョンが異なることが多い。
環境をホストPCに作成する場合、異なるバージョンをどのように管理するか。

### 普通にやる場合
Linuxだと以下のようになるはず

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

※環境によってはpythonコマンドはOS等で使われていたりするのでバージョン変更すると良くないと言われてたりする
昔はpythonがpython2を指していたりしてたので大変だったけど、今は下位互換性あるし大丈夫なのかな？

### pyenv

ちょっと前までは一択。今でもたぶん一番使われているのではないか。
簡単シンプルでPythonのバージョンを変更可能。
https://github.com/pyenv/pyenv

### Dev Container

切り替えが手間なら環境ごと作ればよいじゃない。
https://code.visualstudio.com/docs/devcontainers/containers

`FROM python:3.12` とすれば3.12, `FROM python:3.11` とすれば 3.11。簡単だね。

## 依存ライブラリ管理
Python自体の標準機能はpipで設定ファイルはrequirements.txt（実は名前は何でもよい）

```
pip install requests
pip install -r requirements.txt
```

インストールされるとpython配下のsite-packagesに格納される。
`/usr/local/lib/python3.12/site-packages/`

つまり、違うプロジェクトであっても同じPythonバージョンを使用すると依存ライブラリは共有される
