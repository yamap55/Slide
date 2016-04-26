# ユーザスクリプトのすゝめ

社内勉強会（2016/05/13）
yamap_55

---

以下でスライドを公開しています。
https://slideck.io/github.com/yamap55/Slide/20160513/user_script.md

---

## アジェンダ
1. ユーザスクリプトとは
2. メリット
3. サンプル
4. Chromeの場合
5. Firefoxの場合
6. まとめ

---

## ユーザスクリプトとは

>Webページを開くときに、ブラウザ側で指定しておいたJavaScriptを実行させる機能です。特定のページ（Googleの検索結果など）をカスタマイズして表示したりできます。
>FirefoxのGreasemonkeyが有名ですが、現在は主要ブラウザのほとんどで利用できます。
>[ユーザJavaScript](http://gimite.net/pukiwiki/index.php?%A5%E6%A1%BC%A5%B6JavaScript)

---

有名なユーザスクリプトだと、autopagerやら、マウスジェスチャー、Gmailの見た目変更、便利ボタン追加、ニコニコ動画でほげほげ、テキストボックスに補完候補追加、楽天のメールマガジンのチェックボックスを外したり、JavaScriptのゲームのチートをしたり。。。

---

今では、大体拡張機能があります。

---

では、何故ユーザスクリプトを紹介するのか。

---

簡単に作れる。

---

Chromeの拡張機能も簡単に作れますが、もっと簡単！（Firefoxはちょっと難しい。）

---

ちょっとした所で、ちょっとした事。何回も行うどうでもいい一手間を減らす所で使用したい。

---

具体的には、開発中のアプリケーションのログイン画面で権限別に1クリックでログインしたり、登録画面で適当な値を入力したり、特定のページにショートカット作ったり、面倒な入力を補完したり。

---

## デモ
- [某サイト](https://www.chi-bus.jp/)を開く。
- ユーザスクリプトon。
    - 本来は自動で起動されます。
- [某サイト](https://www.chi-bus.jp/)を開き直す。
- **劇的な変化が！**

---

## コード
```
// ==UserScript==
// @name         New Userscript
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  try to take over the world!
// @author       You
// @match        https://www.chi-bus.jp/
// @require      http://code.jquery.com/jquery-2.2.3.min.js
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
    console.log("quick login start.");
    var list = ["千葉駅","ひまわり幼稚園","中央三丁目"];
    var se = $("<select>").attr({"name":"hoge","id":"hoge"}).on("change",function(){$("input[name='q']").val($(this).val());}).appendTo($(".container-fluid"));
    $.each(list,function(i,v){
        se.append($("<option>").attr({"value":v}).text(v));
    });
    console.log("quick login end.");
})();
```

---

---
