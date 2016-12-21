# SeleniumとGebとPageObjectパターンについて（その1）
勉強会 （2016/12/16）

yamap_55

---

## スライドとか
- スライドは[ここ](https://slideck.io/github.com/yamap55/Slide/20161216/selenium_geb.md)で公開しています。
  - タイトルが大文字に強制変換されてしまうのでそこはスルーしてください。
- 間違えやツッコミがありましたら口頭、[Twitter](https://twitter.com/yamap_55)、[pull request](https://github.com/yamap55/Slide/edit/master/20161216/selenium_geb.md)などお気軽にどうぞ。

---

## PgeObjectパターンとは

> PageObjectデザインパターンとは、アプリケーションの画面を１つのオブジェクトとしてとらえるデザインパターンの１種のことです。Seleniumの公式サイトでも推奨されている、保守性の高いテストコードの書き方です。

---

## PageObjectの原則
- The public methods represent the services that the page offers
  - publicメソッドは、ページが提供するサービスを表す
- Try not to expose the the internals of the page
  - ページの内部を公開しないこと
- Generally don’t make assertions
  - 原則としてassertionを行わないこと
- Methods return other PageObjects
  - メソッドは他のPageObjectsを返す
- Need not represent an entire page
  - ページ全体を表す必要はない
- Different results for the same action are modelled as different as different methods
  - 同じアクションに対して異なる結果となる場合には異なるメソッドとしてモデル化する

---

## 参考
- [Seleniumのコード](https://github.com/yamap55/work/blob/master/20161216_selenium/selenium.groovy)
- [gebのコード](https://github.com/yamap55/work/blob/master/20161216_selenium/geb.groovy)

---

## ご静聴ありがとうございました
