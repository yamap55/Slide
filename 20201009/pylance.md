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

# Pylance について

### yamap55

---

## アジェンダ

- Pylance とは？
- デモ
- 導入時に困った事
- CI でどうやって動かすの？

---

## Pylance とは？

--

- [Visual Studio Code の拡張機能](https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance)

--

- 既存の Python 拡張を補完するもの
- 静的型チェックツールの Pyright を土台に、新しい言語サーバーとして開発
- Microsoft 純正

--

- 関数シグネチャで型情報が表示される
- シンボル上のホバリングにより詳細情報を得られる
- 自動インポート機能
- インストールされた標準ライブラリから適切と思われるモジュールを提案
- 型チェック診断も 2 段階で可能
- IntelliCode、Jupyter Notebooks と互換あり

---

## デモ

※[リポジトリはこちら](https://github.com/yamap55/pylance-sample)

--

- 型設定がされていないフレームワークの補完をしたい場合には stubs を導入する

--

- VSCode の設定の違いを確認

---

## 導入時に困った事

--

### CI でどうやって動かすの？

--

- CLI は提供していないので CI では動かせない
- が、Pyright でチェックすれば OK
- Pyright の設定ファイルもそのまま使える
- Pyright は node のモジュールなのでちょっと面倒

--

### IntelliCode と同居可能？

※IntelliCode も言語サーバの変更が必要であるため

--

- 互換性があるので可能

--

### 型チェックの設定がよくわからない

--

- [Pyright のドキュメント](https://github.com/microsoft/pyright/blob/master/docs/configuration.md)を読む
- 無視したい警告などは設定ファイル（`pyrightconfig.json`）を使用する

---

## 参考

- [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance)
- [開発者の blog](https://devblogs.microsoft.com/python/announcing-pylance-fast-feature-rich-language-support-for-python-in-visual-studio-code/)
