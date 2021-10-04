<style type="text/css">
  .reveal h1,
  .reveal h2,
  .reveal h3,
  .reveal h4,
  .reveal h5,
  .reveal h6 {
    text-transform: none;
  }
  .reveal blockquote p {
    font-size: 32px;
  }
</style>

# Flutter はじめました（パート 2）

---

## アジェンダ

- はじめに
- 環境構築
- チュートリアルの進捗
- build
- GitHub Actions
- 次回予告

---

## はじめに

--

この LT は Flutter をはじめた私が継続して学ぶため、経過報告を行うものです

（LT 駆動開発）

--

## **注意**

- 私はモバイル開発、フロントエンド開発ほぼ経験がありません
- 本スライドの内容は間違っている可能性高いです！
- ツッコミ大歓迎！

--

## リポジトリ

https://github.com/yamap55/flutter_sample

---

## 環境構築

- ローカルに色々入れたくない
- 複数の環境で開発する可能性が高い

--

## Devcontainer を使う！！

--

## Devcontainer とは

- VS Code, Docker さえあれば全て環境を整えられる凄いやつ

--

## Base Image

- 基本となる BaseImage から組み立てるには知識が足りない
- Flutter を触るために作るので何が必要なのか知らない

--

## あった

- [Develop Flutter in a VS Code devcontainer](https://dev.to/matsp/develop-flutter-in-a-vs-code-devcontainer-350g)
- 先人の知恵を借りる
- まあまあ使われているっぽいのでこれを採用
- https://hub.docker.com/r/matspfeiffer/flutter
- https://github.com/matsp/docker-flutter
- （量はないので中身も全部見てます）

--

## ちなみに

- 他にもあって、こちらの方が使われているのでこちらをベースにした方が良いかも？
  - 前述したものは余計な設定、好みではない設定が多い
- https://github.com/cirruslabs/docker-images-flutter
- https://hub.docker.com/r/cirrusci/flutter/

--

## 動かしてみる

---

## チュートリアルの進捗

--

## チュートリアル

- https://flutter.dev/docs/get-started/codelab

--

## 進捗

- あんまり進んでいない
  - あまり時間とれてない
- 最初のページの STEP4 まで

--

## 詳細

- 最初のページ表示
- Hello World 表示
- 依存ライブラリ追加
- ステートフルウィジェットを追加
- 無限にスクロールする ListView を作成

--

## 感想

- 私はあまり Widget には興味がない様子
  - あまりわかっていないからかも？
- バックエンドのロジックは楽しそう
- よくわからないままやるの楽しい

---

## build

--

## 割当タスク

- 実はタスクが割り当てられている
- タスクの内容は CI による build & deploy

--

## 進捗

- ローカルで build
- Docker 上の apache で動かせた！
- つまり、CI で build できれば image 作れそう

---

## GitHub Actions

--

## build

- とりあえず build はできた
- https://github.com/yamap55/flutter_sample/actions/runs/1300602296

--

## 便利な GitHub Actions あった

- Flutter の環境整えてくれる凄いやつ
- https://github.com/marketplace/actions/flutter-action
- https://github.com/subosito/flutter-action

---

## 次回予告

- GitHub Pages にデプロイ
- Docker Image をビルド
- Docker Image を GitHub Packages に push
- チュートリアルをもう少し進める
  - 具体的な数字はなしで。。。

※ここまでできれば上出来

---

## 参考

- [リポジトリ](https://github.com/yamap55/flutter_sample)
- [Develop Flutter in a VS Code devcontainer](https://dev.to/matsp/develop-flutter-in-a-vs-code-devcontainer-350g)
- 使用している Image
  - https://hub.docker.com/r/matspfeiffer/flutter
  - https://github.com/matsp/docker-flutter
- 今後移行したい Image
  - https://github.com/cirruslabs/docker-images-flutter
  - https://hub.docker.com/r/cirrusci/flutter/
- [公式チュートリアル](https://flutter.dev/docs/get-started/codelab)
- [Flutter action](https://github.com/marketplace/actions/flutter-action)（GitHub Actions）
