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
# Databricksとは

---

## アジェンダ
1. 概要
2. 詳細
3. demo
4. 気になる部分
5. デメリット
6. おまけ

---

## 1. 概要

--

### 概要
- Databricks社が運営
    - https://databricks.com/
- Apache Sparkベースの分析サービス
- 最近は[Azure版](https://azure.microsoft.com/ja-jp/services/databricks/)が強い？
    - SEOの問題か検索でよく出てくる

--

### 運営元
- Databricks社
- Apache Sparkの開発者が設立
- 現在でも多数の貢献
    - Spark関連アプリケーション、ライブラリが多数

---

## 2. 詳細

--

### 環境系
- 環境構築が簡単
    1. クラスタ作成
    2. コード書く
    3. 実行
- spark configや環境変数は設定可能
- クラスタの状態やログなどを画面表示

--

### コード系
- Notebook形式
- Python, Scala, R, SQLなどに対応
- コード補完なども少しは

--

### その他
- Sparkの最新機能がいち早く使用可能
    - MLflow
    - Delta Lake
- Notebookの定期実行可能
- APIが充実

--

### お値段
- 無料版はあるがお試しスペック
    - メモリ6GB、インスタンス1、ジョブ実行不可
- EMRの2,3割増し？のお値段
- https://databricks.com/product/aws-pricing/instance-types
- https://aws.amazon.com/jp/emr/pricing/


---

### [3. demo](https://community.cloud.databricks.com/?o=6806233431873777#notebook/2114188653676175)

---

## 4. 気になる所とか

--

### ライブラリインストールは？
- GUIで追加
- ノートブック上でPythonコードで追加

--

### シェルとか叩ける？
- 叩ける
    - 「`%sh`」でいける

--

### PySparkとかよくわからない
- Koalasというライブラリがある
    - https://github.com/databricks/koalas
- PandasライクにSparkのDFを触れる
- Databricks製

---

## 5. デメリット

--

## デメリット
- 日本語が化ける
- 基本的にNotebook形式のみ
- システムへの組み込みは不向き
- クラスタが不安定なことがある

--

### 日本語が化ける
- Hiveのテーブルのコメント
- 他のNotebook呼び出しの引数
- ノートブック名（ファイル名）

--

### 基本的にNotebook形式のみ
- インポート、エクスポートは可能だがDatabricks上ではNotebookに変換される

--

### システムへの組み込みは不向き
- ノートブック形式
- 他のノートブック呼び出しが微妙
    - 「`%run`」、「`dbutils.notebook.run`」を使用
    - 引数が文字列のみ
- Git連携微妙
- 対応策 : [databrick-connect](https://docs.azuredatabricks.net/dev-tools/db-connect.html)
    - databricks上のsparkが使用されるようになる

--

### クラスタが不安定なことがある
- 現場ではたまに重くなりクラスタ再起動を行っている
- 原因は不明
    - AWSやノートブック自体が原因の可能性も？

---

## 6. おまけ

--

### Chrome拡張
- 幾つかChrome拡張あります
- https://chrome.google.com/webstore/search/databricks?hl=ja

--

### 参考
- [公式ドキュメント](https://docs.databricks.com/index.html)

---

## ご清聴ありがとうございました
