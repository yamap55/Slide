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

# ShellCheck の紹介

### yamap55

---

## アジェンダ

- はじめに
- ShellCheck とは
- 使い方
- メモ的な話
- まとめ

---

## はじめに

--

## Shell わかりますか？

--

## Shell をサクッと書けますか？

--

## 私は書けません

--

## そこで ShellCheck

https://github.com/koalaman/shellcheck

---

## ShellCheck とは

--

## シェルスクリプトの静的分析ツール

--

## VSCode Extension 版のデモ

- https://github.com/timonwong/vscode-shellcheck
- https://user-images.githubusercontent.com/29582865/106907134-c299c000-66b2-11eb-8d8b-ea1bd898cb3a.gif

--

## コードチェックの例

https://github.com/koalaman/shellcheck#gallery-of-bad-code

--

## チェックコードの一覧

https://gist.github.com/nicerobot/53cee11ee0abbdc997661e65b348f375#file-_shellcheck-md

---

## 使い方

--

- あらゆるインストール方法が README に書いてある
  - https://github.com/koalaman/shellcheck#installing
- VSCode などのエディタ
- CI
- [Web 版](https://www.shellcheck.net/)

---

## メモ的な話

--

- 基本的にファイルを指定して実行する
- 特定のフォルダ以下全てのシェルに実行等はできないので find と組み合わせる
  - Shell は拡張子や shebang が一意に定まらないため

```bash
find . -type d -name node_modules -prune -o type '*.sh' -print | xargs shellcheck
```

- https://github.com/koalaman/shellcheck/issues/143
- https://github.com/koalaman/shellcheck/wiki/Recursiveness

--

- VSCode 拡張には Quick Fix 機能がある
  - まだお試し中らしい
  - https://github.com/timonwong/vscode-shellcheck#experimental-quick-fix
- コードフォーマットは shfmt というのがある
  - https://github.com/mvdan/sh
- 作者の名前が「koalaman」となかなか愉快
  - https://github.com/koalaman

---

## まとめ

- よくわからないものは外部ツールに頼る
- shell を少しでも使うなら ShellCheck を使う
- ドキュメントたくさん書いてあると嬉しい

---

## ご清聴ありがとうございました
