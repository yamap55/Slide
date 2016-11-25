# Seleniumのすゝめ
勉強会 （2016/11/26）

yamap_55

---

## スライドとか
- スライドは[ここ](https://slideck.io/github.com/yamap55/Slide/20161126/selenium.md)で公開しています。
  - タイトルが大文字に強制変換されてしまうのでそこはスルーしてください。
- 間違えやツッコミがありましたら口頭、[Twitter](https://twitter.com/yamap_55)、[pull request](https://github.com/yamap55/Slide/edit/master/20161126/selenium.md)などお気軽にどうぞ。

---

## Seleniumとは
クロスブラウザ、クロスプラットフォームのUIテストツール

---

## Firefoxの拡張機能だよね？
それらは「Selenium　IDE」や「Selenium Builder」です。

---

## 何が違うの？
Java、C#、Ruby、Python、JavaScriptでコードを書いて、ブラウザを操作します。

---

## どう使うの？
1. ブラウザに合わせたドライバインストール
2. コード書く
3. 実行

---

## ドライバを入れる
- Firefox
    - https://developer.mozilla.org/ja/docs/Mozilla/QA/Marionette/WebDriver
- Chrome
    - https://sites.google.com/a/chromium.org/chromedriver/downloads
    - 32しかないが、64もこれで動かせる。
- IE
    - http://www.seleniumhq.org/download/

---

## コード書く

https://raw.githubusercontent.com/yamap55/work/master/20161118_geb/selenium.groovy

依存性解決が面倒なのでコードはGroovyで書いてますが、Java的に記載。

---

## 結構面倒
- 要素を選択するのがかなり面倒。
- コードが冗長。
- これを保守できる？
  - 実際にはPageObjectパターンというので書くのですが。。。

---

## そこでGeb！


---

## Gebとは
GroovyのSeleniumラッパーフレームワーク

---

## コード

https://raw.githubusercontent.com/yamap55/work/master/20161118_geb/code.groovy

---

## 良いところ
- jQueryライクにセレクタを書ける
- Groovyの機能により細かい事が色々楽。
- PageObjectパターンをサポート。
  - Pageクラスがある
- GroovyのテスティングフレームワークSpockが高機能。

---

## まとめ
- Seleniumは便利だけど使いにくい
- Geb便利
- Groovy便利

---

## ご清聴ありがとうございました
