# BiND HTML制作スキル
## Poni Divers BALI ブログ記事 HTML制作ガイド
**最終更新：2026年3月 | 実装検証済み**

---

## 1. BiNDの主要制約（必ず守ること）

### ❌ 絶対に使ってはいけないタグ・手法

| 禁止事項 | 理由 | 代替策 |
|---------|------|--------|
| `<div>` タグ | BiNDが `<span class="smode">` に変換する。囲みボックスが完全に崩れる | **`<table>`** に統一 |
| `<p>` タグ | BiNDが `.c-lead` クラスを自動付与し、色が `rgb(82,207,245)` に上書きされる | **`<span style="display:block">`** に置換 |
| `display:flex` | BiNDのCSSと干渉してレイアウトが崩れる | **`<table>`** レイアウトに置換 |
| `<style>` タグ | BiNDのhead管理と衝突する | **インラインstyle属性**のみ使用 |
| 外部フォント読み込み（Google Fonts等） | BiND側のフォント設定に任せる | `font-family`にシステムフォントを指定 |
| CSS変数（`var(--color)`） | インラインstyleでは使えない | 色コードを直接記述 |
| `color: xxx !important` | 効果が不安定 | `<span style="display:block; color:#xxx">` で回避 |
| `class` 属性 | BiNDが独自クラスを上書きする | style属性のみ使用 |

---

## 2. BiND検証済みの安全な構造

### ✅ 使えるタグ
```
<table>       → 囲みボックス・レイアウト・H2アイコン行・FAQなど全てに使用
<tr><td>      → レイアウト構造
<span>        → テキスト・インライン要素（display:blockも可）
<h1><h2><h3>  → 見出し（ただしBiNDがスタイルを上書きする可能性あり）
<a>           → リンク
<img>         → 画像
<strong><em>  → 装飾
<ol><ul><li>  → リスト
<hr>          → 区切り線
<br>          → 改行
<thead><tbody><th><td> → テーブル
```

### ✅ 安全なstyleプロパティ
```css
/* 色・背景 */
color: #2c2c2c;
background: #f7fbff;
background: linear-gradient(135deg, #0f2340 0%, #2a7ab5 100%);

/* テキスト */
font-size: 16px;
font-weight: 700;
line-height: 1.85;
font-family: 'Hiragino Kaku Gothic ProN','Meiryo',sans-serif;
letter-spacing: 0.05em;
text-align: center;

/* ボックス */
padding: 22px 24px;
margin: 0 0 24px;
border: 1px solid #dce8f0;
border-left: 4px solid #2a7ab5;
border-radius: 12px;
border-collapse: collapse;
width: 100%;

/* 表示 */
display: block;
display: inline-block;

/* 画像 */
max-width: 100%;
height: auto;
```

---

## 3. 囲みボックスの正しい書き方

### 背景色あり・枠ありボックス（目次・用語解説・参考文献など）
```html
<table style="width:100%; border-collapse:collapse; background:#f7fbff; border:1px solid #dce8f0; border-radius:12px; margin-bottom:44px;">
  <tbody><tr><td style="padding:22px 24px;">
    <span style="display:block; color:#2c2c2c;">テキスト</span>
  </td></tr></tbody>
</table>
```

### グラデーションボックス（ハイライト・CTA・HERO）
```html
<table style="width:100%; border-collapse:collapse; background:linear-gradient(135deg,#1a3a5c 0%,#2a7ab5 100%); border-radius:12px; margin-bottom:24px;">
  <tbody><tr><td style="padding:22px 26px;">
    <span style="display:block; font-size:16px; font-weight:700; color:#ffffff;">タイトル</span>
    <span style="display:block; font-size:14.5px; line-height:1.85; color:#e8f4fd;">本文テキスト</span>
  </td></tr></tbody>
</table>
```

### 左ボーダーボックス（引用・リード文）
```html
<table style="width:100%; border-collapse:collapse; background:#e8f4fd; border-left:4px solid #2a7ab5; border-radius:0 10px 10px 0; margin-bottom:36px;">
  <tbody><tr><td style="padding:22px 24px; font-size:15.5px; line-height:1.9;">
    <span style="display:block; margin:0 0 10px; color:#2c2c2c;">1行目テキスト</span>
    <span style="display:block; color:#2c2c2c;">2行目テキスト</span>
  </td></tr></tbody>
</table>
```

---

## 4. H2見出し（アイコン付き）の正しい書き方
```html
<table style="width:100%; border-collapse:collapse; border-bottom:2px solid #4a9fd4; margin-bottom:24px;">
  <tbody><tr style="vertical-align:middle;">
    <td style="width:52px; padding:0 12px 12px 0;">
      <span style="display:inline-block; width:42px; height:42px; background:#1a3a5c; border-radius:50%; text-align:center; line-height:42px; font-size:20px;">🌕</span>
    </td>
    <td style="padding:0 0 12px;">
      <h2 style="font-size:21px; color:#1a3a5c; font-weight:700; margin:0; line-height:1.5;">見出しテキスト</h2>
    </td>
  </tr></tbody>
</table>
```

**⚠️ アイコン丸は必ず `<span>` で作ること。`<div>` は使わない。**

---

## 5. H3見出しの正しい書き方
```html
<h3 style="font-size:17px; font-weight:700; color:#1a3a5c; margin:0 0 12px; padding-left:14px; border-left:3px solid #4a9fd4; line-height:1.6;">見出しテキスト</h3>
```

---

## 6. FAQの正しい書き方
```html
<table style="width:100%; border-collapse:collapse; border:1px solid #dce8f0; border-radius:10px; margin-bottom:12px; overflow:hidden;">
  <tbody>
    <tr style="background:#1a3a5c; vertical-align:middle;">
      <td style="width:42px; padding:14px 0 14px 16px;">
        <span style="display:inline-block; width:24px; height:24px; background:#f0a500; border-radius:50%; color:#ffffff; text-align:center; line-height:24px; font-size:13px; font-weight:800;">Q</span>
      </td>
      <td style="padding:14px 16px; font-size:15px; font-weight:600; color:#ffffff; line-height:1.5;">質問テキスト</td>
    </tr>
    <tr style="background:#ffffff; vertical-align:top;">
      <td style="padding:14px 0 14px 16px;">
        <span style="display:inline-block; width:24px; height:24px; background:#c8e6f7; border-radius:50%; color:#1a3a5c; text-align:center; line-height:24px; font-size:13px; font-weight:800;">A</span>
      </td>
      <td style="padding:14px 16px; font-size:14.5px; line-height:1.85; color:#2c2c2c;">回答テキスト</td>
    </tr>
  </tbody>
</table>
```

---

## 7. ステップリストの正しい書き方
```html
<table style="width:100%; border-collapse:collapse; margin-bottom:32px;">
  <tbody>
    <tr style="vertical-align:top;">
      <td style="width:44px; padding:0 16px 24px 0;">
        <span style="display:inline-block; width:32px; height:32px; background:#1a3a5c; border-radius:50%; color:#ffffff; text-align:center; line-height:32px; font-size:14px; font-weight:700;">①</span>
      </td>
      <td style="padding:0 0 24px;">
        <span style="display:block; font-size:16px; font-weight:700; color:#1a3a5c; margin:0 0 4px;">ステップタイトル</span>
        <span style="display:block; font-size:14.5px; color:#555555;">ステップ説明文</span>
      </td>
    </tr>
  </tbody>
</table>
```

---

## 8. 画像バナーの正しい書き方
```html
<table style="width:100%; border-collapse:collapse; margin-bottom:36px;">
  <tbody><tr><td style="padding:0; text-align:center; line-height:0;">
    <img
      src="画像URL"
      alt="画像の説明テキスト"
      style="width:100%; max-width:1440px; height:auto; display:block;"
    >
  </td></tr></tbody>
</table>
```

---

## 9. テキストの書き方ルール
```html
<!-- ❌ NG -->
<p style="color:#2c2c2c;">テキスト</p>
<div style="color:#2c2c2c;">テキスト</div>

<!-- ✅ OK -->
<span style="display:block; margin:0 0 16px; color:#2c2c2c;">1段落目</span>
<span style="display:block; margin:0 0 24px; color:#2c2c2c;">2段落目（大きめ余白）</span>
<span style="display:block; color:#2c2c2c;">最終段落</span>
```

---

## 10. 記事全体のラッパー構造
```html
<table style="width:100%; border-collapse:collapse; font-family:'Hiragino Kaku Gothic ProN','Meiryo',sans-serif; font-size:16px; line-height:1.85; color:#2c2c2c;">
  <tbody><tr><td style="padding:0;">

    <!-- ここに記事コンテンツを入れる -->

  </td></tr></tbody>
</table>
```

---

## 11. カラーパレット（Poni Divers BALIブランドカラー）

| 用途 | カラーコード |
|------|------------|
| ネイビーダーク（HERO背景・グラデ起点） | `#0f2340` |
| ネイビー（H2・H3・アイコン背景・FAQ-Q背景） | `#1a3a5c` |
| オーシャン（リンク・ボーダー・グラデ終点） | `#2a7ab5` |
| オーシャンライト（H2アンダーライン・H3左ボーダー） | `#4a9fd4` |
| スカイ（リードボックス背景） | `#e8f4fd` |
| スカイミッド（FAQ-AアイコンBG） | `#c8e6f7` |
| セクションBG（目次・用語解説背景） | `#f7fbff` |
| アクセント（FAQ-Qアイコン・バッジ） | `#f0a500` |
| グリーン（LINEボタン） | `#06c755` |
| 本文テキスト | `#2c2c2c` |
| サブテキスト | `#555555` |
| 枠線 | `#dce8f0` |

---

## 12. BiNDで確認されたその他の挙動

- `<div>` はBiNDが `<span class="smode">` に変換するため**囲みボックスに絶対使用不可**
- `<p>` タグにはBiNDが `.c-lead` クラスを自動付与し `color:rgb(82,207,245)` に上書きされる
- `display:flex` はBiNDのCSSと干渉してレイアウトが崩れる
- `<table>` の `border-radius` はブラウザによって効かない場合あり
- `overflow:hidden` をtableに指定しても効かない場合あり
- BiNDのコンテンツエリア幅は `max-width:960px`・左右padding `30px` で実質 **900px**
- 記事内では `<h1>` はBiNDのページタイトルと競合するため `<h2>` から始めることを推奨

---

## 13. 記事公開前チェックリスト

- [ ] `<div>` タグが0個であること
- [ ] `<p>` タグが0個であること
- [ ] `display:flex` が0個であること
- [ ] `<style>` タグが0個であること
- [ ] 全テキストに `color` が明示されていること
- [ ] 白文字テキストに `color:#ffffff` が明示されていること
- [ ] 全囲みボックスが `<table>` で作られていること
- [ ] アイコン丸が `<span>` で作られていること
- [ ] 外側ラッパーが `<table>` であること
- [ ] BiNDのHTMLブロックに貼り付け後、プレビューで確認すること

---
