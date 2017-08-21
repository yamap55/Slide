# 何かしなきゃと思っているあなたにGroovy
[ビール片手にLT&納涼会 2017](https://jjug.doorkeeper.jp/events/63719) （2017/08/23）
yamap_55

---

## 自己紹介
![icon](../pic/icon.gif)

- Twitter : yamap_55
- Javaっ子。
- Groovy好き
- 7月に転職

---

## 本LTのターゲット
-


- Javaしか使えない人
  - JJUGだし、Javaは使えるよね。。。
- 何かしなきゃと
- 今日、先輩に無理やり連れてこられた

---

## 1から1000までの数値が欲しい
Excel起動しちゃう人

---

## Groovyの7つの使い所

---

## オススメ
- 凄い人がシェルとかperlとか？でやってるどうでもいい事をプログラムで。
- スクリプトで。

---

## 業務内のちょっとした事をGroovyで。
- 凄い人は黒い画面でワンライナーでやっちゃうんだろうな
  - 持っている力（Java力）を使いましょう
- いっぱいあるファイルの特定のレコードをXXする
- テストデータとか
- Excelを読んでファイルを作るとか

---

## 凄い人になる第一歩
- Javaの知識だけで動きます。
- 簡単に改良できます。
- ライブラリ簡単に使えます。

---

## 簡単にレベルアップ
- 普段使っているJava、既に身につけているものの延長
- 簡単に力が伸びる

---

## 簡単？
- Javaが大体そのまま動く
  - 8になってから凄く言いにくい
- Groovyでどう書くのかわからなかったらJavaでかけば良い

---

## Javaのこういうの面倒くさい
- セミコロン
- public static void main
- 例外
- try catch
- ファイル操作
- 外部ライブラリ使用

---

## こういうメソッド欲しい
- 結構な割合でGroovyでは実装されている

---

## マイナーじゃね？
- 意外と使われている。
- Gradle
- Jenkins
- 各種設定ファイル
- 裏では結構使われている
- 先月の[JJUG ナイトセミナー](https://jjug.doorkeeper.jp/events/63161)
![Groovy](https://image.slidesharecdn.com/mybatiswebapplication-170726111305/95/mybatis-web-application-27-638.jpg?cb=1501067651)

---

## 勝手にインストールできない
- groovy-all.jar というjar一個あれば大丈夫。
  - 通常はインストール時についてくるけど、mavenなどで落としてきてそれを使えばOK。

---

## 例
```
java -jar groovy-all-2.4.12.jar hello.groovy
```

---

## Javaをスクリプトとして使う？

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

## CSVを読む
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

## HTTPアクセス
```groovy
@Grab("org.codehaus.groovy.modules.http-builder:http-builder:0.7.1")
import groovyx.net.http.HTTPBuilder

def http = new HTTPBuilder("https://jjug.doorkeeper.jp")
http.get([path : "/events/63719"]) { res, reader ->
  println(reader)
}
```

---

## コマンド実行
```groovy
println "ls".execute().text
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

## Excel
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

## 実績
- 前職
  - 組み込みで使われてた
- 現職
  - メインの言語ではないがバッチ処理やスクリプトで使われている

---

## 何かやらなきゃ！っと焦っていて何もしていないあなた。
## 既にあるJavaをスクリプトとして使ってみませんか？
## 一歩先に進んでみませんか？
## その時にGroovyは強い味方です。
## 多分Groovy界隈の人はきっと色々呟いていてくれるはずです。
## 少なくても私はGroovyに大きな一歩を踏み出す勇気をもらいました。

---

## Groovyが業務で使用されることはないかもしれません。

---

## ただ、一歩を踏み出したいあなたの背中を押してくれます。

---

## Groovyを触ってみてください。

---

## ご清聴ありがとうございました。
