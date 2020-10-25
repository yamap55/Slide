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
- 言語サーバとは？
- デモ
- 導入時に困った事

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

--

- 現在は Python 拡張と Pylance は別の拡張機能だが、将来は統合される予定
- 言語サーバーも統合される予定

--

## [公式ドキュメントの記載](https://github.com/microsoft/pylance-release#features)

- Python拡張に含まれている機能も？

--

<style>
</style>
<span style="font-size:80%">
<ul>
<li>Docstrings</li>
<li>タイプ情報付きの署名ヘルプ</li>
<li>パラメータの提案</li>
<li>コード補完</li>
<li>自動インポート（およびインポートコードアクションの追加と削除）</li>
<li>コードエラーと警告の入力時のレポート（診断）</li>
<li>コードの概要</li>
<li>コードナビゲーション</li>
<li>型チェックモード</li>
<li>ネイティブマルチルートワークスペースのサポート</li>
<li>IntelliCodeの互換性</li>
<li>JupyterNotebooksの互換性</li>
<li>セマンティックハイライト</li>
</ul>
</span>

---

## 言語サーバとは？

--

- エディタ（IDE）で多数のプログラミング言語に対応するのは大変
- エディタ独自に実装が必要
- 実装はエディタが作成されている言語でなされる
  - 移植が大変
  - VSCode は JavaScript、Eclipse は Java など

--

- コード解析処理は別プロセスで動かし、エディタと通信する
  - そもそもコード解析、検証処理は負荷が高い
- 別プロセスで動く部分が言語サーバ
- 言語サーバ自体は様々な言語で記載する事が可能
- 通信するためのプロトコルを言語サーバプロトコル

--

- [Python](https://github.com/microsoft/python-language-server)
  - C# 73.6% Python 26.4%
- [Java](https://github.com/georgewfraser/java-language-server)
  - Java 96.0%
- [PHP](https://github.com/felixfbecker/php-language-server)
  - PHP 99.9%
- [C#](https://github.com/OmniSharp/csharp-language-server-protocol)
  - C# 99.6%
- [TypeScript](https://github.com/theia-ide/typescript-language-server)
  - TypeScript 97.2%

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

--

### Pylance

- [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance)
- [開発者の blog](https://devblogs.microsoft.com/python/announcing-pylance-fast-feature-rich-language-support-for-python-in-visual-studio-code/)

### 言語サーバー

- [language-server-protocol（GitHub）](https://github.com/Microsoft/language-server-protocol)
- [言語サーバープロトコル](https://docs.microsoft.com/ja-jp/visualstudio/extensibility/language-server-protocol?view=vs-2019)
- [What is the Language Server Protocol?](https://microsoft.github.io//language-server-protocol/overviews/lsp/overview/)
