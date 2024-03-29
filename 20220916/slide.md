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

# ローカル環境に依存しない開発環境
- 「VS Code Remote Containers」の話
- 「Cloud IDE」の話

---

## アジェンダ

1. 自己紹介
2. はじめに
3. VS Code Remote Containers
4. クラウドIDE
5. まとめ

---

## 自己紹介

- yamap55
  - ![icon](./icon.gif)
- 職種
  - エンジニア
  - not データアナリスト
- SNS
  - Twitter: [@yamap_55](https://twitter.com/yamap_55)
  - GitHub: [@yamap55](https://github.com/yamap55)

---

## はじめに

--

## 開発環境構築は大変
- バージョン
- 仮想環境
- 依存ライブラリ
- エディターの設定
- 既存環境との相性
- 環境変数
- OS差分
- とかとか

--

### たとえばPythonの場合
- Python2？3？最新版？
- virtualenv
- pyenv
- pipenv
- pathが通ってない

--

### やりたい事はそこじゃない

---

## VS Code Remote Containers

--

## VS Code Remote Containersとは

- Dockerで開発環境作成
- コンテナ内で開発
- コンテナ内でデバック
- ローカルは綺麗なまま
- VS Codeの拡張もコンテナに押し付ける

--

## Dockerとは
<img src="./docker.jpg" style="width:10%;" alt="docker"/>

- ホストマシン上にコンテナという単位の実行環境が作られてアプリケーションを開発・配置・実行するためのプラットフォーム
- ザックリいうとアプリケーション専用の隔離された仮想環境
  - ※厳密な説明ではないです

--

## サンプルも豊富

```
https://github.com/Microsoft/vscode-remote-try-node
https://github.com/Microsoft/vscode-remote-try-python
https://github.com/Microsoft/vscode-remote-try-go
https://github.com/Microsoft/vscode-remote-try-java
https://github.com/Microsoft/vscode-remote-try-dotnetcore
https://github.com/Microsoft/vscode-remote-try-php
https://github.com/Microsoft/vscode-remote-try-rust
https://github.com/Microsoft/vscode-remote-try-cpp
```

--

## 使い方

- `Dockerfile` でコンテナを定義
- `devcontainer.json` で VS Codeの設定を定義

これだけ。


--

## 気になるところ

- Docker、コンテナの知識が多少は必要
- プロジェクトがVS Codeに限定される
  - 最近、[他のエディタでも使えるようになった様子](https://github.com/devcontainers/cli)ではある

--

## デモ

https://github.com/Microsoft/vscode-remote-try-go

<aside class="notes">
1. サンプルをClone
2. VS Codeを開く
    - goの拡張機能は入っていないので、関数コメントとかでない
3. 拡張機能インストール
    - Remote - Containers
4. 左下のアイコンからCloneしたフォルダ開く
    - `C:\github\VS Code-remote\VS Code-remote-try-go`
5. 挙動確認
    - goの関数コメントが出る
        - コンテナ内のVS Codeで拡張機能を入れている
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

## クラウドIDE

--

## クラウドIDE

- なんだかんだホストPCに求められるものが多い
- 近い将来にホストPCはただの箱となると思われる
- Cloud上に開発環境も作る
- ホストからCloud上の開発環境にアクセスして開発を行う

--

## 種類とか

- [AWS Cloud9](https://aws.amazon.com/jp/cloud9/)
  - 独自IDE
- [GitHub Codespaces](https://github.co.jp/features/codespaces)
  - VS Codeベース
  - Visual Studio Onlineは統合されたっぽい
- [Cloud Shell Editor](https://cloud.google.com/shell?hl=ja)
  - Eclipse Theiaベース
- [Gitpod](https://www.gitpod.io/), [PaizaCloudクラウドIDE](https://paiza.cloud/ja/), とか

--

## devcontainerの設定はそのままCodeSpacesに利用可能

- リポジトリから1クリックで開発環境にアクセス
- 新規作成でもワンクリック。
- 必要なものはGitHubのアカウントだけ。

--

## デモ

--

## 注意

- お金はかかる
  - 4core,8GB $0.36/h
- 個人での利用はβ版

---

## まとめ

- 開発環境作成に時間がかからない
- 開発者差分がでない
- ローカル環境に構築→コンテナ利用→Cloud IDE
- 今後開発環境はローカルに作らなくてよいようにしたい

---

## 参考
- [VS Code Remote Containersドキュメント](https://code.visualstudio.com/docs/remote/remote-overview)
- [VS Code Remote Containersサンプルリポジトリ](https://github.com/search?q=org%3Amicrosoft+vscode-remote-try&type=all)
- [Codespaces](https://github.co.jp/features/codespaces)

---

## ご清聴ありがとうございました
