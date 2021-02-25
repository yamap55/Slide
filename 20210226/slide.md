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

# ShellCheckの紹介

### yamap55

---

## アジェンダ

- はじめに
- ShellCheckとは
- 使い方
- まとめ

---

## はじめに

--

## Shellわかりますか？

--

## Shellをサクッと書けますか？

--

## 私は書けません

--

## そこでShellCheck

https://github.com/koalaman/shellcheck


---

## ShellCheckとは

--

## シェルスクリプトの静的分析ツール

--

## VSCode Extension版のデモ

https://github.com/timonwong/vscode-shellcheck
https://user-images.githubusercontent.com/29582865/106907134-c299c000-66b2-11eb-8d8b-ea1bd898cb3a.gif

--

## コードチェックの例

https://github.com/koalaman/shellcheck#gallery-of-bad-code

--

## チェックコードの一覧

https://gist.github.com/nicerobot/53cee11ee0abbdc997661e65b348f375#file-_shellcheck-md

---

## 使い方

--

- あらゆるインストール方法がREADMEに書いてある
  - https://github.com/koalaman/shellcheck#installing
- VSCodeなどのエディタ
- CI
- [Web版](https://www.shellcheck.net/)

---

## メモ的な話
- VSCode拡張にはQuick Fix機能がある
  - まだお試し中らしい
  - https://github.com/timonwong/vscode-shellcheck#experimental-quick-fix
- コードフォーマットはshfmtというのがある
  - https://github.com/mvdan/sh
- 作者の名前が「koalaman」となかなか愉快
  - https://github.com/koalaman

---

## まとめ
- よくわからないものは外部ツールに頼る
- shellを少しでも使うならShellCheckを使う
- ドキュメントたくさん書いてあると嬉しい

---

## ご清聴ありがとうございました
