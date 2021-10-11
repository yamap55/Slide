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

# Flutter はじめました（パート 3）

---

## アジェンダ

- はじめに
- 前回までの振り返り
- GitHub Pages にデプロイ
- まとめ

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

## 前回までの振り返り

--

## 前回まででできたこと

- 環境構築
  - devcontainer
- チュートリアル
  - 少し進めた
- ローカルで build
- GitHub Actions で build

--

## 前回の次回予告

- GitHub Pages にデプロイ
- Docker Image をビルド
- Docker Image を GitHub Packages に push
- チュートリアルをもう少し進める
  - 具体的な数字はなしで。。。

※ここまでできれば上出来

---

## GitHub Pages にデプロイ

→ できた

--

## GitHub Pages

https://yamap55.github.io/flutter_sample/

--

## GitHub Actions 設定

- https://github.com/yamap55/flutter_sample/blob/deploy/github_pages/.github/workflows/build.yaml

--

## 検索は役に立たない

- https://flutter.dev/docs/development/ui/navigation/url-strategies#hosting-a-flutter-app-at-a-non-root-location

※これがほぼ全て

--

## MarketPlace にも Action があるが。。。

- 中身見ると動くかあやしい
  - https://github.com/marketplace/actions/fork-deploy-flutter-web-app-to-github-pages

--

## 中身見ている

- MarketPlace にある Action のソース
  - https://github.com/jeremynac/flutter-gh-pages
- forked from？
  - https://github.com/erickzanardo/flutter-gh-pages
- [Blue Fire](https://github.com/bluefireteam?type=source) という organization に移行したらしい
- これが動きそうだけど、Actions にあるものとは違うものっぽい
  - https://github.com/bluefireteam/flutter-gh-pages
  - 参考にしたのはこのコード

---

## まとめ

- 公式ドキュメントをちゃんと読もう
