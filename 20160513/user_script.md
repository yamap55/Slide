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
3. デモ
4. 作ったもの紹介
5. Chromeの場合
6. Firefoxの場合
7. まとめ

---

## 1. ユーザスクリプトとは

>Webページを開くときに、ブラウザ側で指定しておいたJavaScriptを実行させる機能です。特定のページ（Googleの検索結果など）をカスタマイズして表示したりできます。
>FirefoxのGreasemonkeyが有名ですが、現在は主要ブラウザのほとんどで利用できます。
>[ユーザJavaScript](http://gimite.net/pukiwiki/index.php?%A5%E6%A1%BC%A5%B6JavaScript)

---

有名なユーザスクリプトだと、autopagerやら、マウスジェスチャー、Gmailの見た目変更、便利ボタン追加、ニコニコ動画でほげほげ、テキストボックスに補完候補追加、楽天のメールマガジンのチェックボックスを外したり、JavaScriptのゲームのチートをしたり。。。

---

そういった誰もが不便に思っている事は、大体拡張機能に移行されています。

---

では、何故ユーザスクリプトなのか。

---

## 2. メリット

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

## 4. 作ったもの紹介。
- 勤怠入力システムの入力補助。
- 作成アプリケーションのログイン補助。
- 作成アプリケーションの入力補助。
- 作成アプリケーションの管理画面と入力画面の入れ替え。
- ユーザ登録システムの入力補助。
- 他

---

## 5. Chromeの場合
Chromeはデフォルトでユーザスクリプトをサポートしているので、何もせずに使えますが、[Tampermonkey](http://tampermonkey.net/)という拡張機能を入れると超便利なので入れてください。

（ヘルプデスク承認済み）

---

## 6. Firefoxの場合
一躍ユーザスクリプトを有名にした有名な[Greasemonkey](https://addons.mozilla.org/ja/firefox/addon/greasemonkey/)という拡張機能を導入する必要があります。

---

Chrome、Firefox共に導入手順はwikiに書いてますので、後でメールしますです。（実は1年以上前に。。。）

---

## 7. まとめ

ユーザスクリプトを使用することで、日々の業務内でのちょっとした手間を劇的に改善することができます。



