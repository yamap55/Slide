# lombokのすゝめ
社内勉強会 #13（2016/10/28）
yamap_55

---

## スライドとか
- スライドは[ここ](https://slideck.io/github.com/yamap55/Slide/20161028/lombok.md)で公開しています。
  - タイトルが大文字に強制変換。。。
- コードは[こちら](https://github.com/yamap55/work/tree/master/20161023_lombok/src/main/java/com/yamap55/lombok/slide)
- 間違えやツッコミがありましたら口頭、[Twitter](https://twitter.com/yamap_55)、[pull request](https://github.com/yamap55/Slide/edit/master/20161028/lombok.md)などお気軽にどうぞ。


---

## lombokの読み方

- 読み方 : ロンボック or ロンボク

---

## lombokとは

> lombokは、JavaでのアクセッサやtoString、equalsなどボイラープレートなコードをコンパイル時に生成してくれるライブラリです。

[引用元](http://d.hatena.ne.jp/nowokay/20130730)

---

## ボイラーテンプレートとは
> もともとは活版印刷に使われた鋼板でできた「鋳型（いがた）」のこと

[引用元](https://www.suzukikenichi.com/blog/google%E3%81%AF%E3%80%8C%E3%81%8A%E6%B1%BA%E3%81%BE%E3%82%8A%E3%80%8D%E3%81%8C%E5%AB%8C%E3%81%https://www.suzukikenichi.com/blog/google%E3%81%AF%E3%80%8C%E3%81%8A%E6%B1%BA%E3%81%BE%E3%82%8A%E3%80%8D%E3%81%8C%E5%AB%8C%E3%81%84/84/)

- 定型的なソースコード、断片的な意味で使われる。

---

## @Getter,@Setter
- getterとsetterを自動生成します。

---

## @Getter,@Setter

```java
public class GetterSetterExample {

	public static void main(String[] args) {
		Bean1 bean = new Bean1();
		bean.setId(10);
		bean.setName("ほげ");
		bean.setList(Arrays.asList("a", "b", "c"));

		System.out.println(bean.getId()); // 10
		System.out.println(bean.getName()); // ほげ
		System.out.println(bean.getList()); // [a, b, c]
	}
}

@Getter
@Setter
class Bean1 {
	private int id;
	private String name;
	private List<String> list;
}
```

---

## @NoArgsConstructor、@AllArgsConstructor
- 引数なしコンストラクタを自動生成作成します。
- 全てのフィールドを引数に持つコンストラクタを自動作成します。

---

## @NoArgsConstructor、@AllArgsConstructor

```java
public class ConstructorExample {
	Hoge hoge = new Hoge(10); // 明示的に作成
	Hoge hoge1 = new Hoge(); // @@NoArgsConstructor
	Hoge hoge2 = new Hoge(10, "hoge", new ArrayList<String>()); // @AllArgsConstructor
}

@NoArgsConstructor
@AllArgsConstructor
class Hoge {
	private int id;
	private String name;
	private List<String> list;

	Hoge(int id) {
	}
}
```

---

## @ToString
- toStringを自動生成します。

---

## @ToString

```java
public class ToStringExample {
	public static void main(String[] args) {
		Bean2 bean = new Bean2(10, "hoge", Arrays.asList("a","b"));
		System.out.println(bean.toString()); // Bean2(id=10, name=hoge, list=[a, b])
	}
}

@ToString
@AllArgsConstructor
class Bean2 {
	private int id;
	private String name;
	private List<String> list;
}
```
---

## @EqualsAndHashCode
- フィールドをいい感じに比較するequalsとhashcodeを自動生成します。

---

## @EqualsAndHashCode

```java
public class EqualsToHashCodeExample {

	public static void main(String[] args) {
		Bean4 bean1 = new Bean4(10, "ほげ", Arrays.asList("a", "b", "c"));
		Bean4 bean2 = new Bean4(10, "ほげ", Arrays.asList("a", "b", "c"));

		System.out.println(bean1.equals(bean2)); // true
	}
}

@AllArgsConstructor
@EqualsAndHashCode
class Bean4 {
	private int id;
	private String name;
	private List<String> list;
}
```

---

## @Data
- @ToString、@EqualsAndHashCode、@Getter、@Setter、@RequiredArgsConstructorを同時につけたと同じ。

---

## @Data

```java
public class DataExample {
	public static void main(String[] args) {
		Bean bean = new Bean();
		bean.setId(10);
		bean.setName("ほげ");
		bean.setList(Arrays.asList("a", "b", "c"));

		System.out.println(bean.getId()); // 10
		System.out.println(bean.getName()); // ほげ
		System.out.println(bean.getList()); // [a, b, c]
		System.out.println(bean); // Bean(id=10, name=ほげ, list=[a, b, c])

		Bean bean2 = new Bean();
		bean2.setId(10);
		bean2.setName("ほげ");
		bean2.setList(Arrays.asList("a", "b", "c"));

		System.out.println(bean.equals(bean2));
	}
}

@Data
class Bean {
	private int id;
	private String name;
	private List<String> list;
}
```

---

## @Value
- @Dataのイミュータブル版
- @AllArgsConstructorと同様に全てのフィールドを引数に持つコンストラクタを自動生成します。
- getterのみ自動生成され、setterは生成されない。
- フィールドは全てfinal。

---

## @Value

```java
public class ValueExample {
	public static void main(String[] args) {
		Bean5 bean = new Bean5(10, "ほげ", Arrays.asList("a", "b", "c"));
		// new Bean5(); 未定義
		// bean.setId(10); 未定義

		System.out.println(bean.getId()); // 10
		System.out.println(bean.getName()); // ほげ
		System.out.println(bean.getList()); // [a, b, c]
		System.out.println(bean); // Bean(id=10, name=ほげ, list=[a, b, c])

		Bean5 bean2 = new Bean5(10, "ほげ", Arrays.asList("a", "b", "c"));

		System.out.println(bean.equals(bean2)); // true
	}
}

@Value
class Bean5 {
	private int id;
	private String name;
	private List<String> list;
}
```

---

## val
- JavaScriptやC#のvar、Groovyのdefのような型的な奴

---

## val

```java
public class ValExample {
	public static void main(String[] args) {

		val str = "hoge";
		val i = 42;
		val list = new ArrayList<String>();

		System.out.println(str);
		System.out.println(i);
		System.out.println(list);
	}
}
```

---

## valの注意
- 数年前のバージョンだと色々あったらしいです。
  - Eclipseでコンパイルできるのにjavacではできない
  - 謎のエラー
- 少し使った限りでは再現せず。

---

## 他のアノテーション例
- @NonNull
  - 引数に付与し、nullだったら「ぬるぽ」を投げてくれる。
- @SneakyThrows
  - チェック例外を無視可能。
- @Synchronized
  - 排他制御。
- @Log
  - logという名前のロガー自動生成。

---

## 使い方
1. lombok.jarを取得
  - https://projectlombok.org/download.html
2. ↑を実行（Wクリック）
  - IDEにlombokの設定を追加
3. mavenやgradleで依存関係を追加
4. eclipse:eclipseやgradle eclipseなど
5. IDEにインポート

---

## mavenの設定

```xml
<dependencies>
	<dependency>
		<groupId>org.projectlombok</groupId>
		<artifactId>lombok</artifactId>
		<version>1.16.10</version>
		<scope>provided</scope>
	</dependency>
</dependencies>
```

---

## gradleの設定

```groovy
compileOnly "org.projectlombok:lombok:1.16.10"
```

---

## maven,gradleのスコープ
- provided、compileOnlyとなっている。
- コンパイル時に自動生成されるため、classになった後はlombok.jarは不要。

---

## まとめ
- lombok便利！
- ただ、黒魔術なので使い所は要相談。
  - @Getter,@Setter,@ToString位は簡単に導入できそう。
- valとか使うならJavaを使う必要はない気も。

---

## ちなみにGroovyでは
- 言語仕様で@Getter,@Setter,@AllArgsConstructor,valは対応済み。
- @EqualsAndHashCode、@ToStringは標準ライブラリに含まれています。
- 他にも標準ライブラリに多数存在。（[Package groovy.transform](http://docs.groovy-lang.org/latest/html/gapi/groovy/transform/package-summary.html)）

---

## ちなみにGroovyでは

```groovy
import groovy.transform.ToString
import groovy.transform.EqualsAndHashCode

@EqualsAndHashCode
@ToString
class Bean {
  int id
  String name
}

// Getter, Setter
def bean = new Bean()
bean.id = 10
bean.name = "ほげ"

// @ToString
assert bean.toString() == "Bean(10, ほげ)"

def bean2 = new Bean()
bean2.id = 10
bean2.name = "ほげ"

// @EqualsAndHashCode
assert bean == bean2

// AllArgsConstructor
def bean3 = new Bean([id:20,name:"ふが"])
assert bean3.toString() == "Bean(20, ふが)"
```

---

## 参考URL
- [JavaでIDEのアクセッサ生成よりlombokを使ったほうがいい理由](http://d.hatena.ne.jp/nowokay/20130730)
  - 日本で流行ったのはここから。
- [Lombok 使い方メモ](http://qiita.com/opengl-8080/items/671ffd4bf84fe5e32557)
- [Lombok](http://qiita.com/yyoshikaw/items/32a96332cc12854ca7a3)
- [ScalaとLombokを比べた場合のメリットとデメリット](http://d.hatena.ne.jp/xuwei/20130823/1377231525)
- [JavaでAndroid開発をするなら絶対に導入したいLombok - 超戦士が秘めたる13のパワー[劇場版]](http://qiita.com/oubakiou/items/65bd5e6805ecee0c142a)

---

## ご清聴ありがとうございました
