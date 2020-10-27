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

# Python 標準ライブラリを知る会

### yamap55

---

## アジェンダ

- はじめに
- string
- pdb

---

## はじめに

--

- ここ数カ月で知った内容を共有
- ジャンルバラバラ
- 詳しく知りたい場合はドキュメントを確認

---

## string
一般的な文字列操作

- https://docs.python.org/ja/3/library/string.html#string-constants
- https://github.com/python/cpython/blob/3.9/Lib/string.py

--

```python
whitespace = ' \t\n\r\v\f'
ascii_lowercase = 'abcdefghijklmnopqrstuvwxyz'
ascii_uppercase = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
ascii_letters = ascii_lowercase + ascii_uppercase
digits = '0123456789'
hexdigits = digits + 'abcdef' + 'ABCDEF'
octdigits = '01234567'
punctuation = r"""!"#$%&'()*+,-./:;<=>?@[\]^_`{|}~"""
printable = digits + ascii_letters + punctuation + whitespace
```

--

- ランダムで文字を作成する時など意外と使うことはある
- 自前で定義しても良いが人はミスをする

---

## yyyy

---

## 参考

- [Python 標準ライブラリ](https://docs.python.org/ja/3/library/index.html)
