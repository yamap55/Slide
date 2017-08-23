# 何かしなきゃと思っているあなたにGroovy
[ビール片手にLT&納涼会 2017](https://jjug.doorkeeper.jp/events/63719) （2017/08/23）

yamap_55

---

## 自己紹介
![icon](../pic/icon.gif)

- Twitter : yamap_55
- Javaっ子。
- Groovy好き
- 7月に転職しました。

---

## 本LTのターゲット
- 業務は問題なくこなせる。
- 今のままでいいのかな？🤔
- 何かしなきゃって思っている。😔

---

## みんなすげー
- 私も何かしなきゃ

---

## 何かしなきゃ
- なんでもいい。
- でも、やりたい事特にない。

---

## 何か作る？
- ネタがない😅

---

## 業務内のちょっとした事を楽にしてみよう

---

## ちょっとした事？
- テストデータ作成
- ログファイルから抽出
- DBのデータ確認
- APIでちょっとしたデータ取得

---

## 何使う？
- 新しい事覚えるの辛い。
  - 時間もない。
- 楽したい。😇

---

## Groovyどうですか？

---

## 新しいこと覚えるの辛い
- Javaの知識だけでOK！

---

## HelloWorld.groovy

```Groovy
public class HelloWorld {
  public static void main(String[] args){
    System.out.println("Hello World.");
  }
}
```

---

## 楽したい
- Javaと同じじゃ楽じゃない。

---

## HelloWorld.groovy

```Groovy
println "Hello World."
```

---

## Javaはちょっとした事やるにはちょっと面倒

---

## Javaの面倒な所
- セミコロン
- public static void main
- 例外
- try catch
- ファイル操作
- 外部ライブラリ使用

---

## 全部解決😉

---

## ちょっとした事やってみる

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
println new URL("https://jjug.doorkeeper.jp/events/63719").text
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

## Groovyって流行ってるの？

---

## 流行ってない😂

---

## でも、意外と使われている。
- Gradle
- Jenkins
- Spock
- 各種設定ファイル
- 裏では結構使われている

---

## 先月の[JJUG ナイトセミナー](https://jjug.doorkeeper.jp/events/63161)でも

![Groovy](https://image.slidesharecdn.com/mybatiswebapplication-170726111305/95/mybatis-web-application-27-638.jpg?cb=1501067651)

---

## 勝手にインストールできない
- groovy-all.jar 1個あれば大丈夫。
  - 通常はインストール時についてくるけど、mavenなどで落としてきてそれを使えばOK。

---

## 例
```
java -jar groovy-all-2.4.12.jar hello.groovy
```

---

## 何かやらなきゃ！
## でも。。。というあなた。

---

## Groovyを触ってみてください。

---

## 一歩を踏み出したいあなたの背中を押してくれます。

---

## ご清聴ありがとうございました。🙇
