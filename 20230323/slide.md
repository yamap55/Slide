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

# バージョニングについて

---

## アジェンダ

1. バージョニングとは？
2. なぜ必要？
3. セマンティックバージョニング
4. カレンダーバージョニング
5. 他のバージョニング
6. まとめ

---

## バージョニングとは？

--

## 概要

ソフトウェアやシステムの開発やリリースにおいて、異なるバージョンのソフトウェアを識別するために使用される番号やラベルのこと

--

## 例

- Microsoft Windows 11 Pro 10.0.22621 ビルド 22621
- macOS Monterey 12.6.3
- Chrome 111.0.5563.65
- Notion 2.22.23.12.0.38

とか

---

## なぜ必要？

--

## 特定の状態に名前が付くため

--

## コミュニケーションに有用

- どのバージョンで発生？
- どのバージョンでは発生しない？
- ユーザ、社内、開発チームそれぞれでコミュニケーションが取りやすい

--

## 変履歴管理がしやすい

- どのバージョンに何が実装されているか
- 特定のバージョンに戻す
- 前バージョンとの差分を可視化

---

## [セマンティックバージョニング](https://semver.org/lang/ja/)

※多分一番みるやつ

--

## フォーマット

- `メジャー.マイナー.パッチ`
- 例: v1.2.3
- 例: 4.5.6

--

## メジャーバージョン

- 後方互換性がない変更
- 大きなインパクトのある変更

--

## マイナーバージョン

- 小規模な変更
- 後方互換性がある

--

## パッチ

- バグ修正
- 微細な変更
- 後方互換性がある

--

## 落とし穴

- しっかり運用されていない
- マイナー、パッチで普通に互換性がない
- たまによくある

--

## 開発時の注意

- システムを開発する際には既存のライブラリを使用する
- ライブラリのバージョン管理が必要
  - 1.2.3と2.0.0では破壊的変更が行われている可能性が高いため

--

## 例: npm

- [セマンティックバージョニング](https://docs.npmjs.com/about-semantic-versioning)が推奨されている
- デフォルトでは「^1.2.3」という記載で設定ファイルに記載される
- メジャーバージョンのみ固定される記載方法
- 2.0.0, 1.3.0, 1.2.4 ,1.2.3がある場合には1.3.0が使用される

--

## つまり？

- 1.2.3と書いてあるけど1.3.0を使用する
- 1.3.0なのに互換性がなかった
- 動かない！

---

## [カレンダーバージョニング](https://calver.org/)

※これを知ったのでLTで話してる

--

## なにそれ？

- `年.月.日`
  - 2023.03.23
- 時間を追加
  - 2023.03.23.12
- 一部除去
  - 23.03.23

--

## 直観的

- 意味が一目瞭然
- バージョン付与時に悩みがない

--

## 一意性

- 基本的に重複がない
- 時分秒まで含んでいると安全

--

## 透明性

- リリースの時系列を把握可能
- 最新がどれか
- バージョン比較時にどちらが新しいか

--

## デメリット

- アップデートの影響が不明
  - 大きな変更？小さな変更？
- 長くなりがち

---

## 他のバージョニング

--

## Chromeとか

- 「111.0.5563.65」みたいな形式
- `メジャー.マイナー.ビルド.パッチ`
- 名前はないっぽい

--

## セマンティックバージョニングの派生

- `メジャー・マイナー・パッチ`
- 意味が異なる
- 重要、機能追加、修正程度の指針

--

## 数字が増えていくパターン

- 1,2,3,4,5...
- シンプルイズベスト

--

## ハイブリッドパターン

- セマンティックバージョニングと日付の組み合わせ
- カレンダーバージョニングの末尾に連番
- とか

--

## その他

- α, β, RCとか
- 名前付いていたり

---

## まとめ

--

## まとめ

- バージョンには意味がある
- 適当につければ良いというものではない
- 運用を考えて付ける

---

### ご清聴ありがとうございました
