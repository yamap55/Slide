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

# GitHub の Dependabot が良いよ

### yamap55

---

## アジェンダ

- Dependabot とは
- サンプル
- 注意

---

## Dependabot とは

--

- Library の更新を検知
- Library の更新を PR
  - PR 内にリリースノートなども含む
- GitHub 公式（GitHub が買収）

--

### 細かな設定も可能

- 更新を無視する対象
- レビュアーの指定
- 更新を確認するタイミング

https://docs.github.com/en/github/administering-a-repository/configuration-options-for-dependency-updates

---

## サンプル

- PR
  - https://github.com/yamap55/python_repository_simple/pull/5
- 設定ファイル 1
  - https://github.com/yamap55/python_repository_simple/blob/master/.github/dependabot.yml
- 設定ファイル 2
  - https://github.com/yamap55/atcoder_python_env/blob/master/.github/dependabot.yml

---

## 注意

- GitHub に取り込まれる前は Marketplace で使用する GitHub Apps だったらしい
  - 日本語ドキュメントは Marketplace 版の記載が多い
- 現在は GitHub Actions で使用する
- CI で実行されるユニットテストによって影響を調査するのでユニットテストがほぼ必須

---

## 参考

- https://docs.github.com/en/github/administering-a-repository/keeping-your-dependencies-updated-automatically

---

## ご清聴ありがとうございました
