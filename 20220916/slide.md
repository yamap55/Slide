<style type="text/css">
  .reveal h1,
  .reveal h2,
  .reveal h3,
  .reveal h4,
  .reveal h5,
  .reveal h6 {
    text-transform: none;
  }
</style>

# ローカル環境に依存しない開発環境を作る
「VS Code Remote Containers」の話

---

## 開発環境構築は大変

--

- バージョン
- 仮想環境
- ライブラリ
- エディター
- エディターの設定

--

### たとえばPythonの場合
- Python2？3？最新版？
- virtualenv
- pyenv
- pipenv

--

### やりたい事はそこじゃない

---

## VS Code Remote Containers

--

- Dockerで開発環境作成
- その環境で開発
- その環境でデバック
- ローカルは綺麗なまま
- VSCodeの拡張もコンテナに押し付ける

---

## サンプル
```
git clone https://github.com/Microsoft/vscode-remote-try-node
git clone https://github.com/Microsoft/vscode-remote-try-python
git clone https://github.com/Microsoft/vscode-remote-try-go
git clone https://github.com/Microsoft/vscode-remote-try-java
git clone https://github.com/Microsoft/vscode-remote-try-dotnetcore
git clone https://github.com/Microsoft/vscode-remote-try-php
git clone https://github.com/Microsoft/vscode-remote-try-rust
git clone https://github.com/Microsoft/vscode-remote-try-cpp
```
---

## デモ

<aside class="notes">
1. サンプルをClone
2. VSCodeを開く
    - goの拡張機能は入っていないので、関数コメントとかでない
3. 拡張機能インストール
    - Remote - Containers
4. 左下のアイコンからCloneしたフォルダ開く
    - `C:\github\vscode-remote\vscode-remote-try-go`
5. 挙動確認
    - goの関数コメントが出る
        - コンテナ内のVSCodeで拡張機能を入れている
    - F2で変数名変えてもいい感じに変わる
    - server.goでF5してlocalhost:9000で起動する
6. dockerのプロセス確認
    - `docker ps`
7. 設定ファイル確認
    - `.devcontainer/devcontainer.json` & `Dockerfile`
    - goで少し見せた後、Pythonを見せる
    - go閉じたらコンテナ落ちてる事を確認（`docker ps`）
    - pythonでextensions, settings, postCreateCommandを見せる
</aside>

---

## 思ったこととか

--

- Docker、コンテナの知識が必要
- プロジェクトがVSCodeに限定される
  - PyCharm使いはそれはそれで設定可能っぽい
- ローカルにインストールとか古いという意識を持たなければ

---

## 参考
- [公式ドキュメント](https://code.visualstudio.com/docs/remote/remote-overview)
- サンプルリポジトリ
- [Dockerで立ち上げた開発環境をVS Codeで開く!](https://qiita.com/yoskeoka/items/01c52c069123e0298660)

---

## ご清聴ありがとうございました