<style type="text/css">
  .reveal h1,
  .reveal h2,
  .reveal h3,
  .reveal h4,
  .reveal h5,
  .reveal h6 {
    text-transform: none;
  }
  .reveal blockquote p {
    font-size: 32px;
  }
</style>

# PySpark でハマった件について

---

## アジェンダ

- はじめに
- やりたいこと
- コード
- 障害発生 1
- 障害対応 2
- 障害発生 2
- 解説
- 障害対応 2
- 思ったこと

---

## はじめに

--

- 普段から PySpark 使っている人だとあるあるかも
- PySpark の先生に本件を相談したら一瞬で返事がきた
- 障害調査がこの LT の範囲

---

## やりたいこと

--

## 元データ

| id  | action |
| --- | ------ |
| 1   | A      |
| 1   | A      |
| 1   | B      |
| 2   | A      |
| 2   | C      |
| 2   | C      |
| 3   | B      |

--

## 集計

| id  | action |
| --- | ------ |
| 1   | A      |
| 2   | C      |
| 3   | B      |

※ID 毎に一番多い Action を選択

--

## 別の DF

| id  | type |
| --- | ---- |
| 1   | X    |
| 2   | Y    |
| 3   | Z    |

--

## 最終結果

| id  | action | type |
| --- | ------ | ---- |
| 1   | A      | X    |
| 2   | C      | Y    |
| 3   | B      | Z    |

---

## コード書いていく

--

## 元データの集計

| id  | action |
| --- | ------ |
| 1   | A      |
| 1   | A      |
| 1   | B      |
| 2   | A      |
| 2   | C      |
| 2   | C      |
| 3   | B      |

--

```python
df = (
  spark.read.parquet(path)
  .groupBy('id', 'action').count()
  .withColumn(
    'rank',
    F.row_number().over(
      Window().partitionBy('id').orderBy(F.col('count').desc())
    )
  )
  .where(F.col('rank') == 1)
)
```

※id、action 毎に数えて 1 番多い奴だけを取得

--

## 集計できた

| id  | action |
| --- | ------ |
| 1   | A      |
| 2   | C      |
| 3   | B      |

--

## 別の DF と join

```python
joined_df = df.join(other_df, 'id')
```

--

## join できた

| id  | action | type |
| --- | ------ | ---- |
| 1   | A      | X    |
| 2   | C      | Y    |
| 3   | B      | Z    |

--

# 完

---

## 障害発生 😭

--

## メモリ不足

- 対象の DF は共にかなり大きい
  - 5000 万件以上
- join 時に稀にメモリ不足が起因と思われるエラーが発生
  - 正確には join 後に write すると発生

※ここの調査結果については本 LT の対象外

---

## 障害対応

- join を細かく行って union する
- 元 DF を小さくする事で使用メモリが削減される

※ここの対応策については本 LT の対象外

--

## 細かく join

```python
action_list = ['A', 'B', 'C', 'D', 'E']
l = [
  df.filter(F.col('action') == action).join(other_df, 'id')
  for action in action_list
]
joined_df = reduce(lambda x, y: x.union(y), l)
```

※ここのコードは正しい

---

## 障害発生 😭

--

```python
count1 = joined_df.select('id').distinct().count()
count2 = joined_df.count()
print(count1, count2, count1 - count2)
```

```
954433 999928 -45495
```

※ID が重複している！

--

## 何が悪かったかわかる人！！🙋

---

## 解説

--

ここのコードが良くない

```python
df = (
  spark.read.parquet(path)
  .groupBy('id', 'action').count()
  .withColumn(
    'rank',
    F.row_number().over(
      Window().partitionBy('id').orderBy(F.col('count').desc())
    )
  )
  .where(F.col('rank') == 1)
)
```

※id、action 毎に数えて 1 番多い奴だけを取得

--

## 元データ

| id  | action |
| --- | ------ |
| 1   | A      |
| ... | ...    |
| 5   | A      |
| 5   | B      |
| 5   | C      |

※count が同値になった場合、結果が不定  
※id5 は A、B、C どれが選択されるかわからない

--

## 細かく join する事で表面化

```python
action_list = ['A', 'B', 'C', 'D', 'E']
l = [
  df.filter(F.col('action') == action).join(other_df, 'id')
  for action in action_list
]
joined_df = reduce(lambda x, y: x.union(y), l)
```

--

- PySpark は DF の中身？は遅延評価される
- 集計結果を cache していない
- 細かく join する際、↓ の df が毎回異なる
  - `df.filter(F.col('action') == action)`
- id5 は A の時にも、B の時にも登場するという事が発生する
- 結果的に ID はユニークにならない

--

## おもしろいところ

- 普通に join した時にはこの問題は表面化しない
- df が不定であったとしても 1 回で join すれば ID 重複には繋がらないため

```python
joined_df = df.join(other_df, 'id')
```

---

## 障害対応

--

## `cache()`

```python
df = (
  spark.read.parquet(path)
  .groupBy('id', 'action').count()
  .withColumn(
    'rank',
    F.row_number().over(
      Window().partitionBy('id').orderBy(F.col('count').desc())
    )
  )
  .where(F.col('rank') == 1)
).cache()
```

--

## 結果を固定

- 集計したらそれを固定してしまえば何度使っても同じ値になる

--

## 根本解決

- 本来、解決すべき事項は集計結果が不定である事
- 以下の orderBy で count 以外を含めて固定されるようにすべき

```python
Window().partitionBy('id').orderBy(F.col('count').desc())
```

※が、今回は対応をスキップ。。。

---

## 思ったこと

- レビューで指摘できる気がしない
- 他のプロジェクトではどうしているのか？
