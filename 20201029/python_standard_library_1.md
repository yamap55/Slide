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

> 一般的な文字列操作

っとあるが、固定値を紹介

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

## 使い方例

```python
>>> import string
>>> import random
>>> str_list = random.choices(string.ascii_letters, k=10)
>>> ''.join(str_list)
'FKqioJUmvM'
```

--

- ランダムで文字を作成する時など意外と使うことはある
- 自前で定義しても良いが人はミスをする

---

## pdb

> Python デバッガ

https://docs.python.org/ja/3/library/pdb.html

--

## デバッガとは

> 既知のエラーの原因を突き止め、そのエラーを修正すること

--

VSCode などでブレイクポイント置いたりしますが、スクリプトでデバッグが可能

--

### スクリプト毎

```bash
python -m pdb main.py
```

### コードに組み込む

```python
import pdb; pdb.set_trace()
```

--

jupyter notebook の場合は ↓ を使用するとの事

```python
from IPython.core.debugger import Pdb; Pdb().set_trace()
```

※ほぼ調査していません

---

## 参考

- [Python 標準ライブラリ](https://docs.python.org/ja/3/library/index.html)
