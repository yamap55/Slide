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

# 辞書内包表記で悩んだ件

### yamap55

---

## アジェンダ

- 辞書内包表記とは
- やりたいこと
- 最適解と思われるコード
- 詳細
- 参考

---

## 辞書内包表記とは

--

### こういうやつ

```python
l = ["a", "b"]
d = {s:s for s in l}
assert d == {"a":"a","b":"b"}
```

---

## やりたいこと

--

### これを辞書内包表記で書きたい

```python
l = ["a", "b"]
def f(s):
  k = s * 2
  v = s * 3
  return k, v
d = {}
for s in l:
  k, v = f(s)
  d[k] = v
assert d == {"aa": "aaa", "bb": "bbb"}
```

--

### イメージ

```python
l = ['a', 'b']
def f(s):
  k = s * 2
  v = s * 3
  return k:v # ここ！

d = {f(s) for s in l}
assert d == {"aa": "aaa", "bb": "bbb"}
```

※構文エラーです

---

## 最適解と思われるコード

```python
l = ['a', 'b']
def f(s):
  k = s * 2
  v = s * 3
  return k, v

d = dict([f(s) for s in l])
assert d == {"aa": "aaa", "bb": "bbb"}
```

--

### 補足

- https://docs.python.org/ja/3/library/stdtypes.html#dict

```python
l = [("a","b"), ("c","d")]
d = dict(l)
assert d == {"a": "b", "c": "d"}
```

---

## 詳細？

- `{s:s for s in l}` という「構文」なので関数で返すことはできないと思われる
- 最適解の通り関数では Tuple を返してその List を dict に変換すると思われる

※裏付けできていないので誰か教えて！

---

## 参考とか

- Twitter で悩んだ時のお話
  - https://twitter.com/yamap_55/status/1344640076513304584
- 日本語版 Stack Overflow で聞いてみた
  - https://ja.stackoverflow.com/questions/73132/
- PEP の記載
  - https://www.python.org/dev/peps/pep-0274/

---

## ご清聴ありがとうございました
