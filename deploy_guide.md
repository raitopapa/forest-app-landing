# LP 公開 & note 記事投稿 — 実行手順

LP (landing_page.html) を最速で公開し、note 記事の末尾 CTA を LP の URL に差し替えるまでの手順。

## 前提

- GitHub アカウントを持っている（無ければこの機会に作成）
- note アカウントを持っている（i007955@gmail.com で登録済みを想定）

## 選択肢と推奨

| サービス | 速さ | 独自ドメイン | 推奨度 |
|---|---|---|---|
| Cloudflare Pages | ◎ | ◎ 無料 | ★★★ |
| Vercel | ◎ | ◎ 無料 | ★★☆ |
| Netlify | ○ | ○ 無料 | ★★☆ |
| GitHub Pages | ○ | △ 手間あり | ★☆☆ |

**推奨は Cloudflare Pages**。無料枠が寛大、独自ドメインが無料、日本からも速い。

---

## ルート A: Cloudflare Pages（所要 15 分）

### 1. GitHub リポジトリを作成

```bash
cd C:\Users\i0079\forest-app
git init  # 未初期化なら
mkdir -p landing
cp landing_page.html landing/index.html
git add landing/
git commit -m "feat: add landing page"
```

GitHub で `forest-app-landing` という新規リポジトリを作り、push:

```bash
git remote add origin https://github.com/<username>/forest-app-landing.git
git branch -M main
git push -u origin main
```

### 2. Cloudflare Pages で接続

1. https://dash.cloudflare.com/ にログイン（未登録なら無料アカウント作成）
2. 左メニューの「Workers & Pages」→「Create application」→「Pages」→「Connect to Git」
3. GitHub 連携 → `forest-app-landing` を選択
4. ビルド設定:
   - **Framework preset**: None
   - **Build command**: 空欄
   - **Build output directory**: `landing`
5. 「Save and Deploy」を押す

2 分ほどで `https://forest-app-landing.pages.dev` のような URL が発行される。

### 3. 動作確認

- https://<your-url>.pages.dev をブラウザで開く
- 登録フォームにダミーメールを入力 → 送信 → メーラーが立ち上がり i007955@gmail.com 宛の下書きができることを確認
- スマホでも確認（レスポンシブ）

### 4. 独自ドメインを使う場合（任意）

お名前.com などで `forestapp.jp` のようなドメインを取得（年 1,500 円程度）→ Cloudflare Pages の Custom domains で追加 → DNS 設定。SSL 自動。

---

## ルート B: Vercel（ドラッグ & ドロップで一番早い）

1. https://vercel.com/ にログイン
2. 「Add New...」→「Project」→ `landing_page.html` を `index.html` にリネームしてフォルダごとドラッグ
3. そのまま Deploy

`https://<project>.vercel.app` が即発行される。

---

## note 記事の投稿

### 1. CTA を差し替え

`note_article_web_relaunch.md` の末尾 `https://forestapp.jp/signup` を、発行された LP の URL に書き換える。Ctrl+F で `https://` を検索すれば該当箇所がすぐ見つかる。

### 2. note に投稿

1. https://note.com/ にログイン
2. 右上「投稿」→「テキスト」
3. Markdown をコピペ → note 側でタイトル・見出し・リンクを整形
4. サムネイル画像を設定（推奨: Canva で「林業 × スマホ」のフリー画像で一枚作る）
5. ハッシュタグ: `#森林管理` `#林業` `#DX` `#Flutter` `#個人開発`
6. 公開設定: 「無料で公開」

### 3. 拡散

- 自分の X で「note 書きました」とリンク付き投稿
- 林業関連のコミュニティ（X 上の #林業 タグ、林業 Discord、林業 2.0 など）で共有

### 4. 反応の計測

- note の記事ダッシュボードで PV を毎日確認
- LP 側では Cloudflare Pages の Analytics タブで流入数を確認
- 登録フォーム経由で届いたメール数をカウント

---

## トラブルシュート

**Q. Cloudflare Pages で「Build failed」と出る**
A. Build output directory が合っていない可能性。`landing` フォルダに `index.html` を置いたなら `landing`、ルート直下なら空欄にする。

**Q. フォーム送信しても何も起きない**
A. mailto: はスマホのメーラー未設定端末では動かない。Cloudflare Pages の Forms や Formspree 等の無料フォームサービスに差し替えるのが確実（Phase 1.5 で検討）。

**Q. note 記事の SEO を上げたい**
A. タイトルに「森林管理」「林業」「無料」「クラウド」のどれかを含める。本文冒頭 200 字以内に主要キーワードを散りばめる。

---

## 公開後すぐにやること

1. Google Search Console に LP を登録（sitemap は index.html だけなので任意）
2. note 記事を投稿して X / Facebook の林業コミュニティに共有
3. 登録メールが届き始めたら、返信テンプレを準備（ベータ参加の次ステップ案内）
