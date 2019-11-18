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

# DockerとVSCodeだけで開発環境を作る
「VSCode Remote Containers」を触ってみた

---

## 開発環境って面倒

--

- バージョン
- 仮想環境
- ライブラリ

--

### それぞれ管理するツールとかあるのがまた面倒
- virtualenv
- pyenv
- pipenv

--

### やりたい事はそこじゃない

---

## VSCode Remote Containers

--

- Dockerで開発環境作成
- その環境で開発
- その環境でデバック
- ローカルは綺麗なまま

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

---

## 思ったこととか

--

- Docker、コンテナの知識が必要
- プロジェクトがVSCodeに限定される
  - PyCharm使いはそれはそれで設定可能っぽい
- ローカルにインストールとか古いという意識を持たなければ

---

## ご静聴ありがとうございました
