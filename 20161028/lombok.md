# lombokのすゝめ
社内勉強会（2016/10/28）
yamap_55

---

## スライドとか
- スライドは[ここ](https://slideck.io/github.com/yamap55/Slide/20161028/lombok.md)で公開しています。
- コードは[こちら](https://github.com/yamap55/work/blob/master/20161023_lombok/src/main/java/com/yamap55/lombok/slide/DataExample.java)

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

- そこから、定型的なソースコード、断片的な意味で使われる。

---

## サンプル（@Data）
- getterとsetterの自動生成
  - 片方だけ必要なら「@Getter」、「@Setter」。

---

## サンプル（@Data）

## TODO
@Data = @ToString+@EqualsAndHashCode+@Getter/@Setter+@RequiredArgsConstructor


```java
public class DataExample {
	public static void main(String[] args) {
		Bean bean = new Bean();
		bean.setId(10);
		int id = bean.getId(); // 10
		bean.setName("ほげ");
		String name = bean.getName(); // ほげ
		bean.setList(new ArrayList<String>());
		List<String> list = bean.getList(); // ArrayList
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

## サンプル（@NoArgsConstructor、@AllArgsConstructor）
- 引数なしコンストラクタを作成
- 全てのフィールドを引数に持つコンストラクタを作成

---

## サンプル（@NoArgsConstructor、@AllArgsConstructor）

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

## サンプル（@ToString）
- toStringを自動生成します

---

## サンプル（@ToString）

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

## TODO
- @EqualsAndHashCode
- @Value @Dataの次が良いか？

---

##

---

## サンプル（val）
- JavaScriptやC#のvar、Groovyのdefのような型的な奴

---

## サンプル（val）

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

##

---

##

---

##

---

## 使い方
1. lombok.jarを取得
  - https://projectlombok.org/download.html
2. ↑を実行（Wクリック）
  - IDEにlombokの設定を追加
3. mavenやgradleで依存関係を追加

---

## maven,gradleの設定

- maven

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

- gradle

```groovy
compileOnly "org.projectlombok:lombok:1.16.10"
```

---

##

---

##

---

## まとめ
- lombok便利！
- 黒魔術なので使い所は要相談。

---

##

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
