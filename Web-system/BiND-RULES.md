# BiND実装ルール — Poni Divers BALI

最終更新: 2026年3月

---

## 概要

このドキュメントは、BiND CMS(サイトデザイン社)を使用したPoni Divers BALIウェブサイト制作における実装ルールを定義します。

---

## 1. BiND固有の制約

### 1-1. HTMLタグパーツの制約一覧

| 制約 | 内容 |
|------|------|
| 画像表示 | **不可**。画像はBiND画像ブロックで別配置 |
| CSS記述場所 | 各パーツ内の `<style>` タグに記述 |
| クラス名 | `.poni-` プレフィックス必須(競合防止) |
| JavaScript | 原則不使用(他ブロックと干渉リスク) |
| 外部フォント | BiNDのWebフォント設定を優先 |

### 1-2. 画像の取り扱い

**❌ 禁止:**
```html
<!-- HTMLタグパーツ内での画像表示は不可 -->
<img src="photo.jpg" alt="マンボウ">
```

**✅ 正しい方法:**
```
[BiND 画像ブロック] ← ここで画像を管理
[HTMLタグパーツ]   ← テキスト・CSS・装飾のみ
```

---

## 2. ブロック配置パターン

### 2-1. 画像 + テキストカードの基本構成
```
[BiND 画像ブロック]   ← 写真(alt属性にKW入り日本語テキスト)
[HTMLタグパーツ]     ← テキスト・装飾・タグのみ
[BiND 画像ブロック]
[HTMLタグパーツ]
```

### 2-2. セクション構成例(「選ばれる理由」)
```
① HTMLタグパーツ: セクションヘッダー(eyebrow + H2 + サブテキスト)
② BiND画像ブロック: REASON 01の写真
③ HTMLタグパーツ: REASON 01 テキストカード
④ BiND画像ブロック: REASON 02の写真
⑤ HTMLタグパーツ: REASON 02 テキストカード
⑥ BiND画像ブロック: REASON 03の写真
⑦ HTMLタグパーツ: REASON 03 テキストカード
⑧ HTMLタグパーツ: 口コミバー + CTAボタン
```

---

## 3. 画像ブロック推奨設定

| 項目 | 推奨値 |
|------|-------|
| 角丸 | 上側12px(テキストカードと接続して見せる場合) |
| 縦横比 | 16:9 または 4:3 で統一 |
| altテキスト | KWを含む日本語テキスト(例: 「バリ島マンボウダイビング 日本語スタッフ」) |
| アップロード前処理 | TinyPNGで圧縮・横幅800px推奨 |

---

## 4. CSS実装ルール

### 4-1. CSS記述場所

**各HTMLタグパーツ内の `<style>` タグに記述:**
```html
<div class="poni-card">
  <h3>見出し</h3>
  <p>本文テキスト</p>
</div>

<style>
.poni-card {
  background: #fff;
  padding: 20px;
  border-radius: 8px;
}

.poni-card h3 {
  font-size: clamp(14px, 2vw, 17px);
  margin-bottom: 10px;
}

.poni-card p {
  font-size: 14px;
  line-height: 1.7;
}
</style>
```

### 4-2. クラス命名規則

**必ず `.poni-` プレフィックスを付与:**
```css
/* ✅ 正しい */
.poni-reason-wrap { }
.poni-rc-tag { }
.poni-cta-btn { }

/* ❌ 禁止(他ブロックと競合リスク) */
.card { }
.tag { }
.button { }
```

---

## 5. 文字サイズ設計ルール

### 5-1. サイズ基準表

| 要素 | PC推奨サイズ | SP最小サイズ | **絶対下限** |
|------|------------|------------|------------|
| H2 見出し | clamp(18px, 3vw, 26px) | 18px | **18px** |
| H3 見出し | clamp(14px, 2vw, 17px) | 14px | **14px** |
| 本文テキスト `p` | 14px | 13px | **13px** |
| ボタンテキスト | 14px | 13px | **13px** |
| タグ・バッジ `.rc-tag` 等 | 12px | 11px | **11px** |
| eyebrow・補足・注釈 | 12px | 11px | **11px** |
| **絶対禁止** | — | — | **10px以下** |

### 5-2. clamp()必須箇所の記述例
```css
/* H2 */
h2 {
  font-size: clamp(18px, 3vw, 26px);
}

/* H3 */
h3 {
  font-size: clamp(14px, 2vw, 17px);
}
```

### 5-3. 禁止コード例
```css
/* ❌ 以下はすべて禁止 */
font-size: 9px;
font-size: 10px;
font-size: 0.55rem;  /* 計算結果が10px以下になる */
font-size: 0.6rem;   /* ベース16px想定で9.6px → 禁止 */
```

### 5-4. 根拠
- **SEO**: Googleはモバイルで12px未満のテキストを「読み取り困難」と判定しクロール評価を下げる
- **アクセシビリティ**: WCAG 2.1でモバイル本文の推奨最小サイズは16px
- **UX**: 10px以下は人間の目で読めないレベルであり、ユーザー体験を著しく損なう

---

## 6. JSON-LD挿入方法

### 6-1. BiNDでの実装手順

1. BiNDエディタでページを開く
2. 「ページ設定」→「HTMLタグ追加」を選択
3. 「headタグ内」または「bodyタグ直前」に以下を貼り付け

### 6-2. LocalBusiness構造化データ例
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "Poni Divers BALI",
  "description": "バリ島サヌールの日本語対応ダイビングショップ。PADI 5スター認定。",
  "url": "https://ponidiversbali.com/",
  "telephone": "+62-361-270-381",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "Jl. Hang Tuah No.43",
    "addressLocality": "Sanur",
    "addressRegion": "Bali",
    "postalCode": "80227",
    "addressCountry": "ID"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": "-8.688694",
    "longitude": "115.262894"
  },
  "openingHoursSpecification": {
    "@type": "OpeningHoursSpecification",
    "dayOfWeek": ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"],
    "opens": "07:00",
    "closes": "18:00"
  }
}
</script>
```

### 6-3. FAQPage構造化データ例
```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "バリ島でマンボウは見られますか?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "はい、ヌサペニダ島のクリスタルベイで8〜10月に遭遇率70〜80%で見られます。水深25〜35mの深場で、水温20℃以下の冷水塊に現れるマンボウ(モラモラ)を狙います。"
      }
    },
    {
      "@type": "Question",
      "name": "マンボウダイビングに必要な資格は?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "PADIオープンウォーター以上が必要です。推奨はアドバンス + 経験30本以上。"
      }
    }
  ]
}
</script>
```

---

## 7. CSSクラス命名規則

| クラス名 | 用途 |
|---------|------|
| `.poni-reason-wrap` | セクション全体ラッパー |
| `.poni-reason-eyebrow` | 英字小見出し(Why Choose...) |
| `.poni-reason-h2` | セクションH2 |
| `.poni-reason-sub` | セクションサブテキスト |
| `.poni-rc` | 各理由カード |
| `.poni-rc-head` | カードヘッダー(紺背景) |
| `.poni-rc-num` | REASON 01などのバッジ |
| `.poni-rc-body` | カード本文エリア |
| `.poni-rc-tags` | タグ群ラッパー |
| `.poni-rc-tag` | 個別タグ(水色) |
| `.poni-review-bar` | Googleレビュー誘導バー |
| `.poni-cta-wrap` | CTAエリア全体 |
| `.poni-cta-btn` | CTAボタン |

---

## 8. 過去の失敗事例(再発防止)

| 失敗内容 | 原因 | 対策 |
|---------|------|------|
| HTMLタグパーツ内に `<img>` タグで画像を実装しようとした | BiND制約を失念 | BiND画像ブロックで別配置 |
| imp-badge等に9〜10pxの文字サイズを使用した | 最小サイズ基準が未定義 | 文字サイズ基準表を厳守 |
| クラス名が他ブロックと競合した | プレフィックスなし | `.poni-` プレフィックス必須化 |

---

## 9. チェックリスト

### コード出力前の確認事項

- [ ] HTMLタグパーツ内に `<img>` タグを使用していないか?
- [ ] CSSは `<style>` タグ内に記述しているか?
- [ ] クラス名に `.poni-` プレフィックスを付けているか?
- [ ] 文字サイズは最低基準(本文13px、タグ11px)を満たしているか?
- [ ] 10px以下の文字サイズを使用していないか?
- [ ] clamp()でレスポンシブ対応しているか?

---

## 10. リファレンス

- BiND公式サイト: https://bindup.jp/
- TinyPNG(画像圧縮): https://tinypng.com/
- Schema.org: https://schema.org/
- Google構造化データテストツール: https://search.google.com/test/rich-results

---

**このルールは Poni Divers BALI Webサイト制作プロジェクト専用です。**  
**他のBiNDプロジェクトには適用されません。**
