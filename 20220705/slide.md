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

# SQL用Linter「SQLFluff」

---

## アジェンダ

1. Linterとは
2. SQLFluffとは
3. デモ
4. VS Code拡張機能
5. だめなところ
6. まとめ

---

## Linterとは

--

> Linterは、プログラミングエラー、バグ、スタイルエラー、疑わしい構成にフラグを立てるために使用される静的コード解析ツールです。

https://en.wikipedia.org/wiki/Lint_(software)

--

## もっと簡単に。
- インデントや改行、スペースなど、どうでも良いけど気になるポイントを合わせる
- より良い書き方、セキュリティリスクのある書き方を指摘

--

## Pythonだと

- [flake8](https://flake8.pycqa.org/en/latest/)
- [pylint](https://pylint.pycqa.org/en/latest/)

---

## SQLFluffとは

--

## SQLのLinter
- SQLのLinter
- Jinjaやdbtでも動作するとのこと
  - ~~よく知らない~~
- 自動修正機能もあり
  - autoformatter機能
- 方言に対応

--

## [方言対応](https://github.com/sqlfluff/sqlfluff#dialects-supported)

```
ANSI SQL, BigQuery, ClickHouse, Databricks, Db2, Exasol, Hive, MySQL, Oracle, PostgreSQL, Redshift, Snowflake, SOQL, SparkSQL, SQLite, Teradata, Transact-SQL 
```

--

## 指摘は65種類

https://docs.sqlfluff.com/en/stable/rules.html

※2022/07/04時点の最新である1.0.0の場合

--

## 設定変更可能

- 設定ファイルで設定
  - ある程度はコマンドのオプションでも可能
- ルールの無視
- 例外とする変数
- `,` の位置
- 大文字小文字などルールの設定

---

## デモ

---

## VS Code拡張機能

--

## あるにはあるが。。。

- 更新されていない
  - https://marketplace.visualstudio.com/items?itemName=dorzey.vscode-sqlfluff
  - https://github.com/sqlfluff/vscode-sqlfluff
- fixが動かない
- forkされた拡張機能が乱立
  - https://marketplace.visualstudio.com/search?term=sqlfluff&target=VSCode&category=All%20categories&sortBy=Relevance

--

## 使っているやつ

- [VS Code MarketPlace](https://marketplace.visualstudio.com/items?itemName=RobertOstermann.vscode-sqlfluff-extended)
- [GitHub](https://github.com/RobertOstermann/vscode-sqlfluff-extended)
- まだまだなので色々Issue建てて報告してる


---

## だめなところ

--

## 重い

- 重すぎる
- 500行くらい、指摘が大量のSQLだとかなり時間がかかる
- 1つ修正する度に1から全部実行している？？
- 18ファイルを一括置換して全部fixしたら一生返ってこなかった

--

## fixしても1回で修正されないことがある

- 複数回実行すればOK
- 多分順番にルールを適用させているため

--

## なんでイマイチなの？
- SQLは1970年代に誕生
- 1986年に規格制定
- 35年の歴史でなぜまともなLinterがないのか！

---

## まとめ

--

- LinterとFormatterが1つになっているのは良い
- 事実上標準なので使った方が良い
- 他のLinterに慣れていると不満はある


---

## 参考

- [SQLFluff](https://www.sqlfluff.com/)
- [SQLFluff（GitHub）](https://github.com/sqlfluff/sqlfluff)
- [VS Code拡張機能](https://marketplace.visualstudio.com/items?itemName=RobertOstermann.vscode-sqlfluff-extended)

---

### ご清聴ありがとうございました
