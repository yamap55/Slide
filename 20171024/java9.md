# Java9について
エンジニア勉強会 （2017/10/24）

---

## アジェンダ
- はじめに
- リリースモデル
- Java9での機能追加
- 余談

---

## アジェンダ
- **☆はじめに**
- リリースモデル
- Java9での機能追加
- 余談

---

- 先日、2017/10/21に開催された「
[Java SE 9/EE 8リリースイベント 兼 JavaOne 2017 報告会 @ 東京](https://jjug.doorkeeper.jp/events/66256)」の内容を元に作成されています。
- [YouTubeに動画](https://www.youtube.com/watch?v=XT2tIh9r6Eo)もありますので、詳しく知りたい方はご確認ください。

---

↓で公開しています。
http://yamap55.github.io/Slide/index.html?slide=20171024/java9.md
https://github.com/yamap55/Slide/blob/master/20171024/java9.md

---

## 祝 Java SE 9 リリース
- 2017/09/21にJava SE 9がリリース
- Java SE 8が2014/03/18なので3年半ぶり。

---

## 過去のリリース日

| version |    date    |
|:-------:|:----------:|
|    5    | 2004/09/30 |
|    6    | 2006/12/11 |
|    7    | 2011/07/28 |
|    8    | 2014/03/18 |
|    9    | 2017/09/21 |

---

## 過去最多の追加機能
- 7 : 24
- 8 : 55
- 9 : 91

---

## 元々7で入る機能予定が出揃った
- Project Coin
- Project Lambda
- Project Jigsaw

---

## Javaの方針
- Javaの進化を加速していこう

---

## アジェンダ
- はじめに
- **☆リリースモデル**
- Java9での機能追加
- 余談

---

## リリースモデル
- OpenJDK
- 機能リリース
- サポート
- 更新リリース

---

## Open JDK
- 今まで
  - 仕様のリファレンス実装
  - ソース公開
  - Oracke JDKと技術的な差
- これから
  - Open JDKと技術的な差がなくなる
  - 2018年後半目安

---

## 機能リリース
- 今まで
  - 2年に1度
  - 守れたことない
  - Oracle JDK
- これから
  - 6ヶ月に1度
  - 固定
  - Open JDK

---

## サポート
- 今まで
  - 無償 : 後継バージョンリリース後1年
  - 有償 : 全ての機能リリース
- これから
  - 無償 : 後継バージョンリリース後半年
  - 有償 : 3年毎の機能リリース

---

## 更新リリース
- 今まで
  - 3ヶ月毎
  - メンテナンス用 + 限定的機能アップデート
- これから
  - 3ヶ月毎
  - メンテナンス用

---

![従来のリリースモデル](./release_model_old.png)

---

![新しいリリースモデル](./release_model_new.png)

---

## Oracle JDK
- Oracle JDKはOracle DBのような位置づけになる予定
- 評価、開発では無料で使用できるが、無償で使いたい、今までと同じようにJDKを使いたいならばOpenJDK。
- **ただし、Open JDKはサポートは短い。**

---

## 18.3
- 初の機能リリース版
- 2018/03/20予定

---

![リリースモデルまとめ](./release_model_summary.png)

---

## 移行について
- [Migration Guide](https://docs.oracle.com/javase/9/migrate/toc.htm)の提供あり
- [日本語訳](https://k--kato.github.io/migrating2Jdk9/)もある

---

## サポートの注意
- JDK8のサポートは2018/9まで
- JDK9は2018/3まで
- 18.3は2018/9まで

---

## アジェンダ
- はじめに
- リリースモデル
- **☆Java9での機能追加**
- 余談

---

## Java9での機能追加 1
- REPL導入（JShell）
- モジュール化（Jigsaw）
- ライブラリ改善
  - Collection初期化、Stream機能拡張

---

## Java9での機能追加 2
- セキュリティ強化
  - ALPN対応、DRBG追加、SHA-3対応（1は非対応
- 付属ツールの刷新
  - jcmd（診断ツール）、jhsdb（診断ツール）、jaot（事前コンパイル）など
- G1 GCやコンパイラなどの性能改善
  - G1 GCがデフォルトされたので、省メモリ環境では辛い。
  - → 今までとと同じパラレルGCするようなオプションを付ける。

---

## 今日は以下を紹介
- REPL導入（JShell）
- ライブラリ改善
  - Collection初期化、Stream機能拡張
- モジュール化（Jigsaw）

---

## REPL（JShell）
- JavaのREPL（Read-Eval-Print Loop）ツール
- REPL = れぷる
- 教育分野ではREPLツールがある環境が人気
- REPLがないために、Javaの人気低下
- Web上でも試せる
  - https://tryjshell.org

---

## コマンド
- /help
- /exit
- /list
- /vars
- などが便利

---

## 補完機能
- コード補完
  - Tab
- import補完
  - Shift-Tab i
- 変数定義補完
  - Shift-Tab v

---

## ライブラリ改善
- CollectionのFactory追加
- StreamAPIの強化
- その他

---

## CollectionのFactory追加

---

## 今まで
- Arrays.asList("a","b","c");
- Collections.unmodifiableSet(new HashSet<>(Arrays.asList("a","b","c")));
- new HashMap<>(){{put("k1","v1");put("k2","v2");}};

---

## これから
- List.of("a","b","c");
- Set.of("a","b","c");
- Map.of("k1","v1","k2","v2");

---

## 特徴
- immutable
- フェイルセーフ
  - 例 : nullで例外
  - 例 : Set#ofで重複で例外
- 最適化
  - 要素数が少ない場合には別の実装になっている

---

## StreamAPIの強化
- Stream.dropWhile、takewhile
- Stream.ofNullable
- Stream.iterate

---

## 例 : Stream.takewhile
- 条件を満たしたら終了などが可能に。

```java
IntStream.iterate(0,i->i+1).takeWhile(i -> i < 100).forEach(System.out::println);
```

---

## モジュール化（Jigsaw）

[https://github.com/ykubota/jigsaw-sample_jp](https://github.com/ykubota/jigsaw-sample_jp)

---

## 元の構成

---

```
src
|-- com
|   `-- example
|       `-- server
|           |-- internal
|           |   `-- 内部API.java
|           |-- music
|           |   `-- 音楽API.java
|           `-- open
|               `-- 公開API.java
|-- net
|   `-- example
|       `-- client
|           |-- 公開APIを呼び出す.java
|           `-- 内部APIを呼び出す.java
`-- org
    `-- example
        `-- music
            `-- 音楽をかける.java
```

---

```
% javac -d build -cp . $(find src -name "*java")
% java -cp build net.example.client.公開APIを呼び出す
公開API経由で内部APIを実行
% java -cp build org.example.music.音楽をかける
♪～
# 本来は呼ばせたくない
% java -cp build net.example.client.内部APIを呼び出す
内部APIを実行
```

---

## モジュール化

---

```
src/
|-- server
|   |-- com
|   |   `-- example
|   |       `-- server
|   |           |-- internal
|   |           |   `-- 内部API.java
|   |           |-- music
|   |           |   `-- 音楽API.java
|   |           `-- open
|   |               `-- 公開API.java
|   `-- module-info.java
|-- client
|   |-- net
|   |   `-- example
|   |       `-- client
|   |           `-- 公開APIを呼び出す.java
|   `-- module-info.java
`-- music
    |-- org
    |   `-- example
    |       `-- music
    |           `-- 音楽をかける.java
    `-- module-info.java
```

---

```
% javac -d mods --module-source-path src -m server
% javac -d mods --module-source-path src -m client
% javac -d mods --module-source-path src -m music
```

---

```
% java -p mods -m client/net.example.client.公開APIを呼び出す
公開API経由で内部APIを実行
% java -p mods -m music/org.example.music.音楽をかける
♪～
```

---

## エラー（公開されていないAPIにアクセス）

```
% javac -p mods -d mods/client $(find 01_内部APIの呼び出し/src/client -name "*java")
01_内部APIの呼び出し/src/client/net/example/client/内部APIを呼び出す.java:3: エラー: パッケージcom.example.server.internalは表示不可です
import com.example.server.internal.内部API;
                         ^
  (パッケージcom.example.server.internalはモジュールserverで宣言されていますが、エクスポートされていません)
エラー1個
```

---

## エラー（依存性未定義）

```
% javac -p mods -d mods/music $(find 02_モジュール依存忘れ/src/music -name "*java")
02_モジュール依存忘れ/src/music/org/example/music/音楽をかける.java:3: エラー: パッケージcom.example.server.musicは表示不可です
import com.example.server.music.音楽API;
                         ^
  (パッケージcom.example.server.musicはモジュールserverで宣言されていますが、モジュールmusicに読み込まれていません)
エラー1個
```

---

## 余談（今後）
- Project Amber
  - 18.3
  - varの導入、switchの改良など小さな機能の集まり
- Project Panama
  - ネイティブコードとJava間のデータのやり取り
- Project Valhalla
  - 新しい型であるValue Typeや、ジェネリクスでのプリミティブ型のサポート
- Project Loom（投票中）
  - Continuations Fibers
- Project Metropolis（投票中）
  - hotspotのC++部分をJavaで再実装

---

## 余談（どうでもいい）
```java --version``` でもバージョンが表示されるようになりました。

---

## ちょっと違う

![version](./version.png)

---

## 参考
- [Java 9 and Future #jjug](https://www.slideshare.net/YujiKubota/java9-and-future-jjug)
- [Java SE 9/EE 8リリースイベント 兼 JavaOne 2017 報告会 @ 東京 #jjug #j1jp](https://togetter.com/li/1163158)
- [JJUG JavaOne 2017 報告会のJigsawデモコード](https://github.com/ykubota/jigsaw-sample_jp)
- [新しいリリースモデルはJavaを使う人 全員要注目だった](http://d.hatena.ne.jp/nowokay/20171007#1507284356)
- [Oracle Java SEサポート・ロードマップ](http://www.oracle.com/technetwork/jp/java/eol-135779-ja.html)
- [Faster and Easier Use and Redistribution of Java SE](https://orablogs-jp.blogspot.jp/2017/09/faster-and-easier-use-and.html)

---

## ご清聴ありがとうございました。🙇
