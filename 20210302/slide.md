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

# Pythonの開発環境

### yamap55

---

## アジェンダ

- はじめに
- 各個別設定を紹介
- やっていないこと
- 改善点

---

## はじめに

--

- Pythonでシステムを作る際の開発環境を紹介
- PJメンバーはシステム開発経験が少ない事を想定
  - 環境構築の難易度は低い
  - PJとしての統一を優先
  - 自由度は低い

--

## 参考リポジトリ

https://github.com/yamap55/python_repository_simple

---

## devcontainer

--

- Dockerで開発環境作成
- その環境で開発
- その環境でデバック
- ローカルは綺麗なまま
- VS Codeの設定、拡張機能も統一

--

## 見てみる

https://github.com/yamap55/python_repository_simple/blob/master/.devcontainer/devcontainer.json

--

## 環境構築に時間をかけない

- Git, VS Codeだけあればよい
- VS Codeの設定や拡張機能も設定済み
- Lint, Pytestも動く

--

## 個人の好みの部分は設定可能

- `.vscode/setting.json` は .gitignore に含めている
- 拡張機能もローカルのものが使用可能

--

## ポイント

- 絶対必要なものだけ
  - font、icon、色など個人の好みは設定しない
- 開発者が良いと思ったのはチームで検討して取り入れる
- Python3.8

---

## Flake8

https://github.com/yamap55/python_repository_simple/blob/master/.flake8

--

## ポイント

- 設定は設定ファイルに記載
- docstringを強制
  - flake8-docstrings
- ダブルクォート
  - flake8-quotes
- ファイル保存時に強制起動
- CIで実行

---

## black

--

## ポイント

- 基本はblackに従う
- 1行の文字数だけ緩和
- ファイル保存時に強制起動
- CIで実行
  - チェックだけ

---

## Pylance, Pyright

--

## Pylance

- 色々便利
- [以前の資料](http://yamap55.github.io/Slide/index.html?slide=20201027/pylance.md)

--

## Pyright

- 型チェック
- PylanceはPyrightを内包

--

## ポイント

- Pylanceの補完が便利なので型は基本
- PylanceはVS Codeの拡張機能なのでCIでの実行はPyrightを使用
- Stubを入れる
- まだ、すべては強制できない
  - https://github.com/yamap55/python_repository_simple/blob/master/pyrightconfig.json

--

## Stub？

- Pythonは動的型付け言語
- 型が指定されていないライブラリは多い
- 型を定義可能
- pandasやnumpyもある
  - https://github.com/predictive-analytics-lab/data-science-types

---

## Pytest

https://github.com/yamap55/python_repository_simple/blob/master/pytest.ini

--

## ポイント

- 設定は設定ファイルに記載
- カバレッジ
  - pytest-cov
- 遅いテストを意識
- CIで実行
- ここでは設定していないが、WarningをErrorと扱う事も検討したほうが良い

---

## GitHub Actions

https://github.com/yamap55/python_repository_simple/tree/master/.github/workflows

--

## ポイント
- push時にCIで実行
- PRの画面から遷移しなくてすむように[reviewdog](https://github.com/reviewdog/reviewdog)を活用

---

## Dependabot

https://github.com/yamap55/python_repository_simple/blob/master/.github/dependabot.yml

--

## ポイント
- ライブラリのバージョンはアップデートを忘れがち
- 脆弱性など大きな障害が発生する前にこまめなアップデートを行う

## Docker Compose

https://github.com/yamap55/python_repository_simple/blob/master/docker-compose.yml

--

## ポイント
- RDBなど何らかのアプリケーションを追加する事が多いのでcomposeで構築
- 環境変数はほぼ必ず使用されるので `.env` で管理

---

## ログ設定

https://github.com/yamap55/python_repository_simple/blob/master/logging.conf

--

## ポイント
- 後回しにされがちなので最初に定義
- 形式はini形式だが、yamlやdictはお好み？
  - dictを使用するほうが新しいとのこと

☆★☆★ここから！！！！！☆★☆★

- VS Code
  - 設定
  - 拡張機能
- devcontainer
- Lint
  - flake8
  - black
  - pyright
- Pytest
- GitHub Actions
dependabot.yml
DockerCompose
VS Code拡張機能

---

## やっていないこと
- docstringのbuild


## 改善点
- pip
- pyproject.toml
  - flake8が非対応
- shell, dockerfileなどのlinter追加
  - shellcheck, hadolintなど
- dockerfileに対してDependabot設定
- 拡張機能
- textlint

---

## ご清聴ありがとうございました
