# JavaScriptのObject、Function、prototype、thisについて試行錯誤した私的まとめ
## はじめに
私はWeb業界でプログラマとして生きていたので、何だかんだとJavaScriptを使っています。ただ、Object、Function、prototype、thisをなんとなく使っていました。  
私は普段Javaを使っており、趣味でGroovyを使っています。
それなりにObjectと関数（Function）についてはわかっているつもりでしたが、正直、JavaScriptのObjectとFunctionはよくわからない。

特に以下の辺り。

- 何故に、Functionで定義してるのにnewするのか。
- 「javascript Object」で調べるとfunctionが出てくるのは何故？
- 「Object」という型があるのに何故Functionを使うのか。
- prototypeってどういうこと？
- thisがうまく使えないんだけどｗｗｗ

今回、アロー関数のthisでハマって色々調べたのでまとめます。  
動作確認はChromeの開発者コンソールで行っており、そのままコピペで動作確認できるようにしています。

上記の通り、私はJavaScriptに詳しい訳ではないのでツッコミください。

## Object
- よくあるJavaScriptのObject定義。

```JavaScript
var obj1 = new Object();
obj1.hoge = "hoge";
obj1.huga = function(){console.log("huga");};
obj1.piyo = ()=>{console.log("piyo");};

console.log(obj1.hoge); // hoge
obj1.huga(); // huga
obj1.piyo(); // piyo

var obj2 = {};
obj2.hoge = "hoge";
obj2.huga = function(){console.log("huga");};
obj2.piyo = ()=>{console.log("piyo");};

console.log(obj2.hoge); // hoge
obj2.huga(); // huga
obj2.piyo(); // piyo

var obj3 = {
  hoge:"hoge",
  huga:function() {console.log("huga");},
  piyo:()=>{console.log("piyo");}
}

console.log(obj3.hoge); // hoge
obj3.huga(); // huga
obj3.piyo(); // piyo
```

ここまでは問題ない。

---

ちょっと調べると、JavaScriptはプロトタイプベースとか出てきて、「prototype」でメソッドを定義とか出てくる。
そうかそうか「.」で定義するとかダサいのか。って実際に書いてみるとエラーになる。

```javascript
var obj = {};

// Uncaught TypeError: Cannot set property 'hoge' of undefined(…)
obj.prototype.hoge = "hoge";
```

よく「prototype」でメソッドを定義とかいっている記事を見るとfunctionでオブジェクトを定義している。  
書いてみたら先に進んだけど呼び出したらエラー。

```javascript
var func = function(){};
func.prototype.hoge = "hoge";
console.log(func.hoge); // undefined
```

もっとよく見てみたらnewしている。関数をnewするってどういう事？って思いつつもとりあえず試す。。

```javascript
var func = function(){};
func.prototype.hoge = "hoge";
var obj = new func();
console.log(obj.hoge); // hoge
```

何が起こってるのか理解したいけど、newやprototypeを調べるとカオスなのは既に経験済みなので型を調べてみる。  
functionをnewするとobjectになるらしい。  
ちなみにfunctionの型の事を関数オブジェクトと言うらしい。

つまり、prototypeは関数オブジェクトにあって、オブジェクトにはない。（ちなみにprototypeはオブジェクト）

```javascript
var obj1 = {};
console.log(typeof obj1); // object
var func = function(){};
console.log(typeof func); // function
var obj2 = new func();
console.log(typeof obj2); // object
```

関数といえばECMAScript6で追加されたアロー関数を使えばもっとかっこ良く書けるじゃない。と試すと失敗する。
これはアロー関数の仕様。  
新しい構文を使いからと言ってなんでもかんでもアロー関数に置き換えるとハマる。（どっかに書くだろうけど、thisの扱いも違う。）

```javascript
var func = ()=>"hoge";

//Uncaught TypeError: Cannot set property 'hoge' of undefined(…)
func.prototype.hoge = "hoge";
```

---

関数オブジェクトって言うことはオブジェクトでもあるらしい。  
っということは、メソッド割り当てる事もできる。

```javascript
var obj1 = function(){};
obj1.hoge = "hoge";
obj1.huga = function(){console.log("huga");};
obj1.piyo = ()=>{console.log("piyo");};

console.log(obj1.hoge); // hoge
obj1.huga(); // huga
obj1.piyo(); // piyo
```


---

ここからメモ書き。上は全部書き直す。

クラスとオブジェクトをごっちゃにしていた事が原因。
当たり前だけどクラスとオブジェクトは別。

Javaだとstaticを除いて、オブジェクトを使用する場合にはnewすることでインスタンスを作ってから使用するため、
任意のオブジェクトを作る = クラスの作成 となってしまっていた。

よく考えると上記した通り、クラスとオブジェクトは別物（2回目）。
Javaだってクラスはオブジェクトなので、当たり前。

JavaScriptの場合、{}やnew Object()と使用することでオブジェクトを直接作成可能。
そのオブジェクトに「obj.hoge = 関数」と言った形でメソッドを紐付けていく。

一方、クラスとは。

> クラスとは、オブジェクト指向プログラミングにおいて、データとその操作手順であるメソッドをまとめたオブジェクトの雛型を定義したもの。

っという事なので、データをコンストラクタで渡してその操作手順をメソッドで定義する。
つまり、クラスをnewしてインスタンスを使用すれば良いと。

ECMAScript 2015（ECMAScript 6は通称。）でclassが追加される。
```javascript
class Human {
  constructor(name) {
    this.name = name;
  }
  hello() {
    console.log('My name is ' + this.name);
  }
}
obj = new Human('yamap_55');
obj.hello(); // My name is yamap_55
```

これは新しいClassという概念が追加されたわけではなく、
いい感じに書けるようになったというだけで、内部的にはprototypeを使用しているという事らしい。
ただ、同名のclassを定義しようとしたらエラーとなったので、この辺りはいい感じ。

```javascript
class hoge{}
class hoge{} // Uncaught TypeError: Identifier 'hoge' has already been declared
```


## 参考
- [や...やっと理解できた！JavaScriptのプロトタイプチェーン](http://maeharin.hatenablog.com/entry/20130215/javascript_prototype_chain)
- [オブジェクトリテラルのプロパティ/メソッドのいろんな書き方（ES6版](http://qiita.com/kura07/items/356bd37733f457d3177f)
- [Google流 JavaScript におけるクラス定義の実現方法](http://www.yunabe.jp/docs/javascript_class_in_google.html)
