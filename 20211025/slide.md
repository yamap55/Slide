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

# Flutter はじめました（パート 4）

---

## アジェンダ

- はじめに
- 前回までの振り返り
- 本番リポジトリで devcontainer
- ローカルで build
- Docker で動かす
- ARISE 開発環境
- チュートリアル
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
- チュートリアル（少し
- ローカルで build
- GitHub Actions で build
- GitHub Pages にデプロイ
- Docker Image をビルド
- Docker Image を GitHub Packages に push

--

## やりたい事はほぼ全てできた

※**サンプルコードで。**

---

## 本番リポジトリで devcontainer

- できたにはできたが、色々辛い
- 既存のものを無理やり使っていたが、新たに 1 から作った

--

## Windows では難しい部分がある

- Docker とはいえ、ホストの OS の影響はある
- Windows の場合シンボリック・リンクは管理者でないと使えない
- バージョン管理等でシンボリックリンクを張るようなアプリケーションは相性が悪い
  - pyenv、npm とか

--

## fvm は辛い

- flutter のバージョン管理を行う[fvm](https://github.com/leoafarias/fvm)は、バージョンを切り替えをシンボリックリンクで実現している様子。
- 回避できなかった
- 使用しなくても問題ない事を確認

---

## ローカルで build

- 動いてはいる
- firebase の emulator と連携ができていない？

---

## Docker で動かす

- 動いてはいる
- 構文エラーが出る
  - ほんと意味不明

---

## ARISE 開発環境

- 検証環境かと思っていたら本番環境として使う想定だったらしい
- よく考えたら VPN 通してないとアクセスできない事が発覚
- DaaS 内で直接アクセスできないと使えないので何とかしたい

---

## チュートリアル

- 進捗 0
- チュートリアルページすら開いていない。。。

---

## まとめ

- 外側だけでも中身わかっていないと大変！
- インフラエンジニアの人ほんと尊敬する。

--

## 雑談的な奴

- Flutter は必要なものが多い？ので image が重い
- HDD 枯渇
- 開発 PC を検討 → シン環境になりそう
- 来年には新環境で開発できそう！
