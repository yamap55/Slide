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

# Pythonの開発環境

### yamap55

---

## アジェンダ

- はじめに
- CHECK 制約とは
- 試してみた
- 実装状況
- 思った事

---

## はじめに

--

- Pythonでシステムを作る際の開発環境を紹介
- PJメンバはシステム開発経験は少ない事を想定
  - 環境構築の難易度は低い
  - PJとしての統一を優先
  - 自由度は低い

--

## 参考リポジトリ

https://github.com/yamap55/python_repository_simple

---

## devcontainer

--

- Dockerで開発環境作成
- その環境で開発
- その環境でデバック
- ローカルは綺麗なまま
- VSCodeの設定、拡張機能も統一

--

## 見てみる

https://github.com/yamap55/python_repository_simple/blob/master/.devcontainer/devcontainer.json

--

## 環境構築に時間をかけない

- Git, VSCodeだけあればよい
- VSCodeの設定や拡張機能も設定済み
- Lint, Pytestも動く

--

## 個人の好みの部分は設定可能

- `.vscode/setting.json` は.gitignoreに含めている
- 拡張機能もローカルのものが使用可能

--

## ポイント

- 絶対必要なものだけ
  - font,icon,色など個人の好みは設定しない
- 開発者が良いと思ったのはチームで検討して取り入れる

---

## Flake8

https://github.com/yamap55/python_repository_simple/blob/master/.flake8

--

## ポイント

- 設定は設定ファイルに記載
- docstringを強制
  - flake8-docstrings
- ダブルクォート
  - flake8-quotes
- ファイル保存時に強制起動
- CIで実行

---

## black

--

## ポイント

- 基本はblackに従う
- 1行の文字数だけ緩和
- ファイル保存時に強制起動
- CIで実行
  - チェックだけ

---

## Pylance, Pyright

--

## Pylance

- 色々便利
- [以前の資料](http://yamap55.github.io/Slide/index.html?slide=20201027/pylance.md)

--

## Pyright

- 型チェック
- PylanceはPyrightを内包

--

## ポイント

- Pylanceの補完が便利なので型は基本
- PylanceはVSCodeの拡張機能なのでCIでの実行はPyrightを使用
- Stubを入れる
- まだ全ては強制できない

--

## Stub？

- Pythonは動的型付け言語
- 型が指定されていないライブラリは多い
- 型を定義可能
- pandasやnumpyもある
  - https://github.com/predictive-analytics-lab/data-science-types

---

## Pytest

https://github.com/yamap55/python_repository_simple/blob/master/pytest.ini

--

## ポイント

- カバレッジ
  - pytest-cov
- 遅いテストを意識
- CIで実行

---

## GitHub Actions

https://github.com/yamap55/python_repository_simple/tree/master/.github/workflows

--

## ポイント
- push時にCIで実行
- PRの画面から遷移しなくてすむように[reviewdog](https://github.com/reviewdog/reviewdog)を活用

---

## Dependabot

https://github.com/yamap55/python_repository_simple/blob/master/.github/dependabot.yml

--

## ポイント
- ライブラリのバージョンはアップデータ忘れがち
- 脆弱性など大きな障害に繋がる前にこまめなアップデートを行う

## Docker Compose

https://github.com/yamap55/python_repository_simple/blob/master/docker-compose.yml

--

## ポイント
- RDBなど何らかのアプリケーションが追加される事が多いのでcomposeで構築
- 環境変数はほぼ必ず使用されるので `.env` で管理

---


☆★☆★ここから！！！！！☆★☆★

- VSCode
  - 設定
  - 拡張機能
- devcontainer
- Lint
  - flake8
  - black
  - pyright
- Pytest
- GitHub Actions
dependabot.yml
DockerCompose
VSCode拡張機能

---

## 改善点
- pip
- pyproject.toml
  - flake8が非対応
- shell, dockerfileなどのlinter追加
  - shellcheck, hadolintなど
- dockerfileに対してDependabot設定
- 拡張機能

## ある日のつぶやき

![tweet1](./img2.png)

--

## リプライ

![tweet2](./img3.png)

--

## CHECK 制約！？

---

## CHECK 制約とは

--

## Wikipedia

> CHECK 制約 （-せいやく、英: Check Constraint）とは、データベースにおいてデータを追加、更新する際の有効なデータを定義する規則のことをいう。

https://ja.wikipedia.org/wiki/CHECK%E5%88%B6%E7%B4%84

--

## SQL 規約

- SQL92 で既定されている
- SQL92 = 1992 年 11 月が初版
- 詳細
  - http://www.contrib.andrew.cmu.edu/~shadow/sql/sql1992.txt
  - https://en.wikipedia.org/wiki/SQL-92

--

## 基本構文

```sql
CREATE TABLE products (
    product_no INT,
    name TEXT,
    price NUMERIC CHECK (price > 0)
);
```

https://www.postgresql.jp/document/9.4/html/ddl-constraints.html

--

## 名前付き複数列

```sql
CREATE TABLE Persons (
    ID INT NOT NULL,
    LastName VARCHAR(255) NOT NULL,
    FirstName VARCHAR(255),
    Age INT,
    City VARCHAR(255),
    CONSTRAINT CHK_Person CHECK (Age>=18 AND City='Sandnes')
);
```

---

## 試してみた

--

## 実行 SQL

```
CREATE TABLE users (
  age INT CHECK(
    age >= 18
    AND age < 100
  ),
  name VARCHAR(10) CHECK(
    name ~ '^a'
  )
);
```

```
INSERT INTO users VALUES(17, 'a');
INSERT INTO users VALUES(18, 'b');
INSERT INTO users VALUES(18, 'a');
```

--

## 実行結果

![checkキャプチャ](./img1.png)

---

## 実装状況

--

## PostgreSQL

少なくても 7.3.21 では実装済み（2008 年 1 月 7 日）

https://www.postgresql.org/docs/7.3/ddl-constraints.html

--

## MySQL

8.0.16 で対応（2019 年 4 月 25 日）
https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-16.html#mysqld-8-0-16-sql-syntax

--

- Oracle
  - https://docs.oracle.com/cd/E16338_01/server.112/b56299/clauses002.htm
- SQL Server
  - https://docs.microsoft.com/ja-jp/sql/relational-databases/tables/create-check-constraints?view=sql-server-ver15
- DB2
  - https://www.ibm.com/support/producthub/db2/docs/content/SSEPGG_11.5.0/com.ibm.db2.luw.admin.dbobj.doc/doc/c0020152.html

--

- 主要 Database は対応している
- MySQL が一番遅かった様子

---

## 思った事

--

- 少しでも RDB 触るのであれば知らないのはやばい
- どこまで定義するのか難しい
  - ガチガチに設定は少し違うお気持ち
  - やりすぎると緩和緩和と変更対応大変そう
  - 結局は最後の網として使用？

---

## 参考 1

- 概要
  - https://ja.wikipedia.org/wiki/CHECK%E5%88%B6%E7%B4%84
- SQL92
  - http://www.contrib.andrew.cmu.edu/~shadow/sql/sql1992.txt
  - https://en.wikipedia.org/wiki/SQL-92

--

## 参考 2

- RDB ドキュメント
  - PostgreSQL
    - https://www.postgresql.jp/document/9.4/html/ddl-constraints.html
  - MySQL
    - https://dev.mysql.com/doc/refman/8.0/en/create-table-check-constraints.html
  - Oracle
    - https://docs.oracle.com/cd/E16338_01/server.112/b56299/clauses002.htm
  - SQL Server
    - https://docs.microsoft.com/ja-jp/sql/relational-databases/tables/create-check-constraints?view=sql-server-ver15
  - DB2
    - https://www.ibm.com/support/producthub/db2/docs/content/SSEPGG_11.5.0/com.ibm.db2.luw.admin.dbobj.doc/doc/c0020152.html

---

## ご清聴ありがとうございました
