# JavaScriptのObject、Functionについて

社内勉強会 #5 （2016/07/08）  
yamap_55

---

以下でスライドを公開しています。
https://slideck.io/github.com/yamap55/Slide/20160708/javascript.md

---

## はじめに
JavaScriptは、オブジェクトとクラス、関数についてよくわからない！！

ので、まとめました。

---

## オブジェクト

```javascript
var obj1 = new Object();
obj1.hoge = "hoge";
obj1.huga = function(){console.log("huga");};
obj1.piyo = ()=>{console.log("piyo");};

console.log(obj1.hoge); // hoge
obj1.huga(); // huga
obj1.piyo(); // piyo

// こんな定義や
var obj2 = {};

// こんな定義もできる。
var obj3 = {
  hoge:"hoge",
  huga:function() {console.log("huga");},
  piyo:()=>{console.log("piyo");}
}
```

---

## クラス定義

```javascript
// コンストラクタ
var Func = function(){};

// メソッド定義
Func.prototype.hoge = "hoge";
Func.prototype.huga = function(){console.log("huga");};
Func.prototype.piyo = ()=>{console.log("piyo");};

// インスタンス（オブジェクト）作成
var obj = new Func();
console.log(obj.hoge); // hoge
obj.huga();
obj.piyo();
```

---

## クラス定義 別解
```javascript
var Func = function(){
  // メソッド定義
  this.hoge = "hoge";
  this.huga = function(){console.log("huga");};
  this.piyo = ()=>{console.log("piyo");};
};

// インスタンス（オブジェクト）作成
var obj = new Func();
console.log(obj.hoge); // hoge
obj.huga();
obj.piyo();
```

---

## オブジェクトとクラスの型
```javascript
var obj1 = {};
console.log(typeof obj1); // object
var func = function(){};
console.log(typeof func); // function
var obj2 = new func();
console.log(typeof obj2); // object
```

---

## わかりにくいところ？

**メソッド定義とクラス定義は同じfunctionを使用する。**
よって、こんな事ができてしまう。

```javascript
var Func = function(){};
Func.prototype.huga = function(){console.log("huga");};
var obj = new Func();

// メソッドをnewできちゃう。
var hugahuga = new obj.huga();
```

---

## アロー関数のコンストラクタ
ES6で追加されたアロー関数使うことで対応可能。

```javascript
var Func = function(){};
Func.prototype.huga = ()=>console.log("huga");
var obj = new Func();

// Uncaught TypeError: obj.huga is not a constructor
var hugahuga = new obj.huga();
```

---

## アロー関数のprototype

```javascript
var Func = function(){};
Func.prototype.huga = function(){console.log("huga");};
var obj = new Func();

// メソッドをnewできちゃう。
obj.huga.prototype // undefined
```

---

## アロー関数の「this」には注意
じゃぁ、何でもかんでもアロー関数にすればいいかというとそうでもない。
JavaScriptの基本に忠実で、「this」に注意！

```javascript
var Hoge = function() {
  this.name = "hogehoge";
  this.getNameArrow = function(){return this.name};
  this.getNameFunction = () => {return this.neme};
}

var hoge = new Hoge();
console.log(hoge.getNameArrow()); // hogehoge
console.log(hoge.getNameFunction()); // undefined
```

---

## アロー関数の「this」

通常のfunctionの「this」は呼び出し先の「this」になりますが、
アロー関数の「this」は呼び出し元の「this」が使用されます。

先の例だとfunctionの場合はインスタンスがthisになり、アロー関数の場合はwindowがthisになります。

---

## 個人的なハマりどころとか1
- クラスとオブジェクトをごっちゃにしていた事が原因。
- 当たり前だけどクラスとオブジェクトは別。
- Javaだとstaticを除いて、オブジェクトを使用する場合にはnewすることでインスタンスを作ってから使用するため、任意のオブジェクトを作る = クラスの作成 となってしまっていた。

---

## 個人的なハマりどころとか2
- よく考えると上記した通り、クラスとオブジェクトは別物（2回目）。
- Javaだってクラスはオブジェクトなので、当たり前。
- JavaScriptの場合、{}やnew Object()と使用することでオブジェクトを直接作成可能な所が理解できていなかった。
- オブジェクトに「obj.hoge = 関数」と言った形でメソッドを紐付けていく。

---

## 個人的なハマりどころとか3
- 一方、クラスとは。

> クラスとは、オブジェクト指向プログラミングにおいて、データとその操作手順であるメソッドをまとめたオブジェクトの雛型を定義したもの。

- っという事なので、データをコンストラクタで渡してその操作手順をメソッドで定義する。
- つまり、クラスをnewしてインスタンスを使用すれば良いと。

---

## 参考
- [や...やっと理解できた！JavaScriptのプロトタイプチェーン](http://maeharin.hatenablog.com/entry/20130215/javascript_prototype_chain)
- [オブジェクトリテラルのプロパティ/メソッドのいろんな書き方（ES6版](http://qiita.com/kura07/items/356bd37733f457d3177f)
- [Google流 JavaScript におけるクラス定義の実現方法](http://www.yunabe.jp/docs/javascript_class_in_google.html)

---

## ご静聴ありがとうございました。
