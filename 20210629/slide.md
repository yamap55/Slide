<style type="text/css">
  .reveal h1,
  .reveal h2,
  .reveal h3,
  .reveal h4,
  .reveal h5,
  .reveal h6 {
    text-transform: none;
  }
  table {font-size: 25px}
</style>

# システム設計勉強会第 7 回

---

## アジェンダ

- はじめに
- テーブル設計が悪いとプログラムの変更が大変
- データベース設計をすっきりさせる
- コトに注目するデータベース設計
- 参照をわかりやすくする工夫
- オブジェクトの設計とテーブル設計
- 参考

---

## はじめに

--

<img src="./img/img01.png" style="width:40%;" alt="現場で役立つシステム設計の原則"/>

https://www.amazon.co.jp/dp/B073GSDBGT/

--

## 第 6 章 データベースの設計とドメインオブジェクト

- テーブル設計が悪いとプログラムの変更が大変
- データベース設計をすっきりさせる
- コトに注目するデータベース設計
- 参照をわかりやすくする工夫
- オブジェクトの設計とテーブル設計

--

### 注意

- 本勉強会では「第 5 章 アプリケーション機能を組み立てる」はスキップ
- 参加者にアプリケーション、3 層の話が中心でアプリケーションを作成するチームも含まれるため
- データベースとは RDB を想定している
- 分析で使用するデータマートとは異なる
  - が、共通する点は多い

---

## テーブル設計が悪いとプログラムの変更が大変

--

## menu

- → **テーブル設計が悪いとプログラムの変更が大変**
- データベース設計をすっきりさせる
- コトに注目するデータベース設計
- 参照をわかりやすくする工夫
- オブジェクトの設計とテーブル設計

--

## データベースあるある

- どこにどのようなデータが入っているのかわからない
- データが入っていないカラムが多い
- データが重複していて、どのデータが正しいかわからない
- 1 つのカラムがさまざまな目的で使用されている
- テーブル間の関係がはっきりしない

--

## 問題が発生するデータベース

- 用途がわかりにくいカラム
- 色々な用途に使う巨大なテーブル
- テーブルの関係がわかりにくい

--

### 用途がわかりにくいカラム

- カラム名が省略形
- NULL 値が入ったカラム
- 他のカラムの内容によって値の意味が変わる
- 値をプログラムで分割する必要がある
- 意味を読み取れないコードがついている
  - マジックナンバーとか

※自由項目、予備項目などのカラムが最悪

--

### 色々な用途に使う巨大なテーブル

- 似たようなカラムが多く、使い分け方がわからない
- 用途によっては使われないカラムがある
  - NULL 値が多くなる

--

### テーブルの関係がわかりにくい

- 外部キー制約がない
- キーとなるカラムの名前に一貫性がない

---

## データベース設計をすっきりさせる

--

## menu

- テーブル設計が悪いとプログラムの変更が大変
- → **データベース設計をすっきりさせる**
- コトに注目するデータベース設計
- 参照をわかりやすくする工夫
- オブジェクトの設計とテーブル設計

--

### 基本的な工夫を丁寧に実践する

- 名前を省略しない
- 適切なデータ型を使う
  - サイズも定義
- 制約をきちんと使う

--

### NOT NULL 制約が導くテーブル設計

- NULL は「未知」
- データベースは「既知」の値を記録するもの
- NULL 逃れをしない（unknown, 9999, -1 とか）
- 別テーブルに分ける

--

### 一意性制約でデータの重複を防ぐ

- 1 つの事実に 2 つのレコードは異常
- どのカラムの組み合わせで一意になるかを意識する

--

### 外部キー制約でテーブル間の関係を明確にする

- テーブルを分割した際にテーブル間の関係を意識する
- 関係を記録する事を強制する方法が外部キー制約

---

## コトに注目するデータベース設計

--

## menu

- テーブル設計が悪いとプログラムの変更が大変
- データベース設計をすっきりさせる
- → **コトに注目するデータベース設計**
- 参照をわかりやすくする工夫
- オブジェクトの設計とテーブル設計

--

### 業務アプリケーションの関心事は「コト」の管理

- 現実に起きたコトの管理
- 将来起きるコトの記録

--

### 「コト」の管理のための制約

- NOT NULL 制約
  - 起きたコトの記録に不明はおかしい
  - 記録があるべき場所に記録がないとプログラムは正しく動作しない
- 一意性制約
  - 1 つのコトが 2 つ記録されていてはいけない
- 外部キー制約
  - コトとして記録された複数のテーブルの関係を明確にする

--

### ヒトやモノとの関係を正確に記録するための 3 つの工夫

1. 記録のタイミングが異なるデータはテーブルを分ける
   - 同一テーブルでは NULL が混入する
2. 記録の変更を禁止する
   - 過去のコトの記録を変更するべきではない
   - 元データ、取り消しデータ、新データの 3 レコードで表現する
3. カラムの追加はテーブルを追加する
   - NULL が混入 or 虚のデータが登録される

--

### 少し余談

- `CRUD is dead` （死んだのは U と D）という話が以前あった
- 論理削除（delete flag）とも関連がある？
- 絶対的に不変なマスター以外はイベントとして扱うという理解
- 社員データもマスターではなくイベントデータ
  - 退職や転籍などが発生するため

---

## 参照をわかりやすくする工夫

--

## menu

- テーブル設計が悪いとプログラムの変更が大変
- データベース設計をすっきりさせる
- コトに注目するデータベース設計
- → **参照をわかりやすくする工夫**
- オブジェクトの設計とテーブル設計

--

### コトの記録に注力したテーブル設計の問題

- カラム数の少ないテーブルが多数必要
- 必要な情報を得るために多くのテーブルを結合する必要がある
- 現在の状態を直接参照できない

--

### 状態の参照

- 基本はコトの記録のテーブル
- コトの記録のたびに「状態を管理するテーブル」を更新
- 状態を更新するテーブルはコトの記録のテーブルからいつでも再構築可能な二次的な導出データ

--

### UPDATE 文は使わない

- UPDATE 文はデータの不整合が混入しやすい
  - 記録の同時性に違反（NULL の発生）
- DELETE & INSERT を使用する
  - レコードの存在を意識する必要もない

--

### コトの記録と状態の更新は同時である必要はない

- 厳密なトランザクションとして処理されるべきではない
  - 状態の更新が失敗した場合にコトの記録を取り消すのは間違っている
- 同時である必要がないのであれば別システムに任せる選択肢がある
  - 処理の独立性が高まる
  - システムの設計がシンプルになる

※NoSQL などで出てくる結果整合性と理解

--

### 状態の更新は 1 箇所でなくても良い

- 状態の更新を複数のサーバで行う事も可能
  - 例: 売上が発生（コト）した事を通知
    - 顧客管理サーバで顧客の売上を更新
    - 営業管理サーバで部門の売上を更新
- 非同期メッセージングが便利

--

### 派生的な情報を転記して作成する

- コトの発生を起点として必要に応じて処理を平行で行う
  - 集計、複製、サブセットなど
- イベントソーシング
  - [イベント・ソーシングを知る](https://www.slideshare.net/shuheifujita90/ss-14294169)
- 問題点
  - 厳密な即時性、派生データ間の整合性の保証には仕組みが必要

--

### コトの記録から状態を動的に導出する

- 未来の状態のシミュレーションが可能
- 過去の状態を再現可能
  - テストや障害再現などで有用

---

## オブジェクトの設計とテーブル設計

--

## menu

- テーブル設計が悪いとプログラムの変更が大変
- データベース設計をすっきりさせる
- コトに注目するデータベース設計
- 参照をわかりやすくする工夫
- → **オブジェクトの設計とテーブル設計**

--

### オブジェクトとテーブルは似てくる

- 似てくるが同じものではない

--

### 異なるものとして明示的にマッピング

| 特性             | オブジェクト                 | テーブル                   |
| ---------------- | ---------------------------- | -------------------------- |
| 目的             | データと **ロジック** の整理 | データの整理               |
| 関心毎           | 導出や加工、判断             | 導出や加工の元になるデータ |
| アプローチ       | 部品から全体                 | 全体から部分               |
| 設計変更のリズム | 頻繁                         | ゆるやか                   |

--

### オブジェクトはオブジェクトらしく

- 別々で設計と改善を進める
- マッピングは進度を合わせて明示的に定義する

--

### 業務ロジックはオブジェクト、事実の記録はテーブル

- ドメインオブジェクトは業務の関心毎を整理
- データベースは事実を正しく記録する

---

## まとめ

--

- 制約のないデータベースがプログラムを複雑にする
- 制約を徹底する
- NOT NULL 制約、一意制約、外部キー制約
- コトの記録の徹底
- 状態の更新はコトの記録と分離
- オブジェクトとテーブルは異なる

---

## 参考

- 現場で役立つシステム設計の原則
  - https://www.amazon.co.jp/dp/B073GSDBGT/
- CRUD is dead への質問（link が有用）
  - https://teratail.com/questions/46605
- イベント・ソーシングを知る
  - https://www.slideshare.net/shuheifujita90/ss-14294169
- マイクロサービスにおける結果整合性との戦い
  - https://www.slideshare.net/ota42y/ss-112380848
- 非同期処理と疎結合ができる「メッセージング」の常識
  - https://www.atmarkit.co.jp/ait/articles/1001/08/news121.html
