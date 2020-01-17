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

# Apache Groovy
### というプログラミング言語の紹介

---

## 多分皆様は触る事はないでしょう

---

## なんで紹介するの？

---

## 私が成長するきっかけになったプログラミング言語

---

## 私が好きだから

LTってそういう所。

---

## 何それ？

> Groovy（グルービー）は、Javaプラットフォーム上で動作する動的プログラミング言語である。

参考 : [Wikipedia](https://ja.wikipedia.org/wiki/Groovy)

---

## Javaプラットフォーム？

> Javaプラットフォームは Javaで記述されたプログラムの開発および実行を行うことのできるソフトウェア群の総称である。

参考 : [Wikipedia](https://ja.wikipedia.org/wiki/Java%E3%83%97%E3%83%A9%E3%83%83%E3%83%88%E3%83%95%E3%82%A9%E3%83%BC%E3%83%A0)

---

## JVM（Java Virtual Machine）
Javaはコードを書いたら（xx.java）をコンパイルして（xx.class）JVM上で動かす。
- 各環境にJVMがあればどこでもJavaが動く
- xx.classにコンパイルできればなんでも動く
- Javaの資源をそのまま使える

---

## JVM言語

- Java
- Scala
- Kotlin
- Groovy

---

## 他の言語も動く
- JRuby（Ruby）
- Jython（Python）
- Clojure（Lisp）
- Rhino（JavaScript）

---

## 最近はGraalVMが流行っているのでお察し

---

## 話を戻します

---

## 人気あるの？

- [TIOBE Index](https://www.tiobe.com/tiobe-index/) 2020年1月
    - 23位（参考 : Scala 32位、Kotlin 35位）
- [redmonk](https://redmonk.com/sogrady/2019/03/20/language-rankings-1-19/) 2019年1月
    - 24位（参考 : Scala 13位、Kotlin 20位）
- [IEEE](https://spectrum.ieee.org/static/interactive-the-top-programming-languages-2019) 2019年
    - 38位（参考 : Scala 18位、Kotlin 24位）

---

## 日本ではほぼ聞かない

---

## が、現職も前職も使ってた
派手さはないが地味に使われているかも。

---

## 何か有名なツールとかある？
- Jenkins（一部）
    - CIツール
- Gradle
    - Java系のビルドツール
---

## Javaの面倒な所
- セミコロン
- public static void main
- 例外
- try catch
- ファイル操作
- 外部ライブラリ使用

---

## さくっと書ける
- Javaで書くには面倒な部分で使われる
- JVM言語のツールへの組み込み
- JavaのユニットテストをGroovyで

---

## Javaのスクリプト言語なので本当の意味でJavaScript

って本書いてる人が言ってた。

---

## フレームワークなどもある
- Grails
    - フルスタックフレームワーク

---

## コードとか紹介

---

## File読み込み
## 全部読む
```groovy
new File("test.txt").text
```

---

## 一行づつ読む
```groovy
new File("test.txt").eachLine {
  println it
}
```

---

## ファイル書き込み

```groovy
new File("text.txt") << "hogehoge"
```

---

## HTTPアクセス
```groovy
println new URL("https://ja.wikipedia.org/wiki/Groovy").text
```

---

## コマンド実行
```groovy
println "ls".execute().text
```

---

## CSVを読む
- こんなファイル

```csv
columnA,columnB,columnC
hoge1,huga1,piyo1
hoge2,huga2,piyo2
hoge3,huga3,piyo3
```

---

## CSVを読む
```groovy
@Grab('com.xlson.groovycsv:groovycsv:1.1')
import com.xlson.groovycsv.CsvParser

def csv = new File("test.csv")
def data = new CsvParser().parse(csv.text, separator: ',')
data.each {
  println "${it.columnA} : ${it.columnB} : ${it.columnC}"
}
```

---

## DB接続
```groovy
@Grapes([
  @Grab("com.h2database:h2:1.4.196"),
  @GrabConfig(systemClassLoader = true),
])
import groovy.sql.Sql

def db = Sql.newInstance("jdbc:h2:mem:", "org.h2.Driver")
db.execute("create table sample(id int)")
db.executeUpdate("insert into sample(id) values (99)")
println db.rows("select * from sample")
```

---

## Excel操作
```groovy
@Grapes([
  @GrabResolver(name="bintray", root="http://dl.bintray.com/nobeans/maven"),
  @Grab("org.jggug.kobo:gexcelapi:0.5"),
])
import org.jggug.kobo.gexcelapi.GExcel

def path = $/C:\work\hoge.xlsx/$
def book = GExcel.open(path)
def sheet = book["sheet1"]
sheet.rows.each {
  println "${it[0].value} : ${it[1]}"
}
```
---

## まとめ
いつかどこかでJava使う事があって、ちょっとJavaだと面倒という事があれば、 *Apache Groovy* を思い出してください

---

## ご清聴ありがとうございました
