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

# GitHub Packages

---

## アジェンダ

- GitHub Packages とは
- コンテナレジストリ
- 触ってみる
- まとめ

---

[以前も LT で話してたらしい](http://yamap55.github.io/Slide/index.html?slide=20200124/GitHub_Packages.md)（2020/01/24）

---

## GitHub Packages とは

--

## [概要](https://docs.github.com/en/packages/learn-github-packages/introduction-to-github-packages)

- ソフトウェアパッケージのホスティングサービス
- 2019/11/13 に正式サービス化
  - GitHub Actions と同時
- 旧名 : GitHub Package Registry
- npm,gem,mvn,gradle,docker,dotnet cli をサポート

--

## メリット

- 既存のサービスと遜色なく使える
- GitHub のサービスなので GitHub と相性抜群
  - GitHub Actions のサポートも手厚い
- [料金](https://docs.github.com/ja/billing/managing-billing-for-github-packages/about-billing-for-github-packages)
  - public は無料
  - private リポジトリでも使用可能（容量厳しめ？）
  - GitHub 自体が有料プランであれば緩和

--

## デメリット

- 世界に公開するとなると既存サービスの方が有利
  - リポジトリの追加など別途設定が必要
- 公式以外は情報があまりない

※Microsoft によってデメリットが減りつつある

---

## コンテナレジストリ

--

## 2021/06/21 に正式リリース

> 2019/11/13 に正式サービス化

実は docker だけは β だった

--

## GitHub Package Registry と統合

- `docker.pkg.github.com` が順次 `ghcr.io` に移行される

--

## 削除可能に変更

- 以前は削除不可だったためサンプルなどが残ってしまった
  - https://github.com/yamap55?tab=packages
- 2021 年の 2-3 月辺りに変更
- ダウンロード数が 25 以下のイメージは削除可能

--

## 他

- ランディングページの作成
- 権限制御
- 匿名アクセス
  - public の場合、GitHub 認証が不要

---

## 触ってみる

--

## 手順

- docker login
  - GitHub の token が必要
- docker build
- docker push

--

## GitHub Action

- Action が用意されているのでかなり楽
  - [公式サンプル](https://docs.github.com/en/actions/guides/publishing-docker-images#publishing-images-to-github-packages)
  - [試した](https://github.com/yamap55/github_package_test/blob/master/.github/workflows/publish_docker_image.yml)

※LT で言いたかったのはここだけ  
※ `docker/metadata-action` が結構凄い

---

## まとめ

- GitHub Actions 含めても超簡単に使える
- 無料アカウントで private で使う場合には容量に注意
- package 本体とコード（リポジトリ）が紐づくのはわかりやすい

---

## 参考

- [Your packages, at home with their code](https://github.com/features/packages)
- [GitHub Packages](https://docs.github.com/ja/packages)
- [Introduction to GitHub Packages](https://docs.github.com/en/packages/learn-github-packages/introduction-to-github-packages)
