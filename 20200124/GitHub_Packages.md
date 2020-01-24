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

# GitHub Packages

---

- ソフトウェアパッケージのホスティングサービス
- 昨年11/13に正式サービス化
- 旧名 : GitHub Package Registry
- GitHub Actionsの影に隠れてあまり話題になってない
- npm,gem,mvn,gradle,docker,dotnet cliをサポート

---

## メリット
- 既存のサービスと遜色なく使える
- GitHubのサービスなのでGitHubと相性抜群
- privateリポジトリの場合はGitHubとセットなので有利
  - DockerHubなど外部サービスは別途費用がかかる

---

## デメリット
- 世界に公開するとなると既存サービスの方が有利
  - 各ツールでデフォルトとなっているため
- ドキュメントは充実しているが、中途半端に日本語になっていてわかりづらい
- 公式以外は情報があまりない
- 検索すると古い情報が出てくるので注意

---

## docker
- docker login
- docker build
- docker push

--

### 実例
```
docker login docker.pkg.github.com -u yamap55 -p 8982f91d09e95dda471d67ff9f68408eed9adc8c
docker build -t docker.pkg.github.com/yamap55/github-package-registry-sample/sample-img:1.0 .
docker push docker.pkg.github.com/yamap55/github-package-registry-sample/sample-img:1.0
```

※[GitHubで確認](https://github.com/yamap55/github-package-registry-sample/packages)

--

### 使い方

- docker pull
```
docker pull docker.pkg.github.com/yamap55/github-package-registry-sample/sample-img:1.0
```
- dockerfile
```
FROM docker.pkg.github.com/yamap55/github-package-registry-sample/sample-img:1.0
```

---

## 参考
- [GitHub Packages](https://github.com/features/packages)
- [About GitHub Packages](https://help.github.com/en/github/managing-packages-with-github-packages/about-github-packages)
- [Using GitHub Packages with your project's ecosystem](https://help.github.com/en/github/managing-packages-with-github-packages/using-github-packages-with-your-projects-ecosystem)

---

## ご清聴ありがとうございました
