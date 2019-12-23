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

# 最近行った開発環境の整備について

---

## 話すこと
- VSCode Remote Containers
- GitHub Actions
- Github Package Registry

---

## VSCode Remote Containers

--

## 開発環境って面倒

--

- バージョン
- 仮想環境
- ライブラリ
- エディタ

--

### 例えば
- Python2？3？
- virtualenv
- pyenv
- pipenv

--

### やりたい事はそこじゃない

--

## VSCode Remote Containers

--

- Dockerで開発環境作成
- その環境で開発
- その環境でデバック
- ローカルは綺麗なまま
- VSCodeの拡張もコンテナに押し付ける

--

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

--

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

--

## 思ったこととか

--

- Docker、コンテナの知識が必要
- エディタがVSCodeに限定される
  - PyCharm使いはそれはそれで設定可能っぽい
- ローカルにインストールとか古いという意識を持つ

--

## 参考
- [公式ドキュメント](https://code.visualstudio.com/docs/remote/remote-overview)
- サンプルリポジトリ
- [Dockerで立ち上げた開発環境をVS Codeで開く!](https://qiita.com/yoskeoka/items/01c52c069123e0298660)

---

## GitHub Actions

--

- 先日11/13に正式サービス化
- GitHubの公式CI
- GitHubのサービスなのでGitHubとの連携が楽
  - Tokenとか指定不要

--

普通にCIとして使える以上に特に言うことはないので割愛 🙇

---

## Github Package Registry

--

- ソフトウェアパッケージのホスティングサービス
- 先月11/13に正式サービス化
- GitHub Actionsの影に隠れてあまり話題になってない
- npm,gem,mvn,gradle,docker,dotcetをサポート

--

### メリット
- 既存のサービスと遜色なく使える
- GitHubのサービスなのでGitHubと相性抜群
- privateリポジトリの場合はGitHubとセットなので有利
  - DockerHubなど別途費用がかかる場合がある

--

### デメリット
- 現在では世界に公開するとなると既存サービスの方が有利
  - 各ツールでデフォルトとなっているため
- ドキュメントは充実しているが、中途半端に日本語になっていてわかりづらい
- 公式以外は情報があまりない
- 検索すると古い情報が出てくるので注意

--

## デモ

---

## まとめ

--

- 開発環境の統一は便利
- GitHubを使い倒そう

---

## ご静聴ありがとうございました
