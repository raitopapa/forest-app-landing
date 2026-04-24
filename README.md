# forest-app-landing

[森林管理サービス](https://github.com/raitopapa/forest-app) のランディングページ。

## 構成

- `landing/index.html` — 本体（シングルファイル、CSS/JS インライン）
- `deploy_guide.md` — 公開手順（Cloudflare Pages / Vercel）

## ローカルで開く

```
open landing/index.html
```

または任意の静的サーバーで。

## 公開

Cloudflare Pages に接続する場合:

- Build command: （なし）
- Build output directory: `landing`

詳細は [deploy_guide.md](./deploy_guide.md) を参照。

## 登録フォーム

`mailto:` で shinrin.app@gmail.com に届く仕様。
将来的に Formspree 等への差し替えを想定。

## 関連

- 本体コード: https://github.com/raitopapa/forest-app
- ブランチ: `web-support`（Flutter Web 対応作業中）
- note 記事: （投稿後リンク追記）
