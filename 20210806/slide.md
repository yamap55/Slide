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

# flake8-bugbear

---

## アジェンダ

- はじめに
- flake8-bugbear とは
- チェック内容
- まとめ
- 参考

---

## はじめに

--

## flake8 とは

コードに対して基本的な品質をチェックするツール。
コードの構文をチェックしてよろしくない部分を指摘してくれます。

--

## 何が良いの？

- 構文エラー、タイプミス、不適切なフォーマット、誤ったスタイルなどを防ぐことができる
- 開発者の時間を節約する
- コードレビュー者の時間を節約する
- 無料
- 導入が簡単

--

## flake8 には拡張機能がある

flake8 単体でも優れたツールですが、フレームワークや PJ などに合わせた独自のチェックを追加する事ができます。

--

## flake8 の拡張機能例

- flake8-isort
- flake8-quotes
- flake8-django
- flake8-docstrings

などなど

https://github.com/DmytroLitvinov/awesome-flake8-extensions

--

## flake8-bugbear

flake8 の拡張機能の 1 つとして今回紹介する「flake8-bugbear」があります

---

## flake8-bugbear とは

--

> プログラムのバグや設計上の問題の可能性を見つけるためのプラグイン。pyflakes および pycodestyle に属さない警告が含まれています

https://github.com/PyCQA/flake8-bugbear

--

## 開発元

個人のプロジェクトではなく PyCQA（Python Code Quality Authority）に含まれているので、信頼性は高い。
flake8 や isort、pylint や pycodestyle なども含まれている。

https://github.com/PyCQA

---

## チェック内容

https://github.com/PyCQA/flake8-bugbear#list-of-warnings

※全 17 種類 + α

--

## コード書いてみました

https://github.com/yamap55/flake8-bugbear-sample

※動かす環境付き

--

## 公式リポジトリにサンプルあります！

https://github.com/PyCQA/flake8-bugbear/tree/master/tests

※動かす環境が不要であればこちらを参照してください

---

## まとめ

- 信頼性の高い開発元
- 細かいチェックしてくれるので有用
- 邪魔になるようなものもないので flake8 とセットで導入すべき

---

## 参考

- [flake8-bugbear のリポジトリ](https://github.com/PyCQA/flake8-bugbear)
- [公式のサンプル](https://github.com/PyCQA/flake8-bugbear/tree/master/tests)
