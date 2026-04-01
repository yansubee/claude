# BiND HTML制作スキル v2
## Poni Divers BALI ブログ記事 デザイン仕様 & HTMLテンプレート
**最終更新：2026年4月 | 残留窒素記事で検証済み**

> v1（BiND_HTML制作スキル.md）はBiND制約・禁止タグ・構造ルールの基礎資料。
> v2（本ファイル）はPoni Divers BALIブランドのデザイン仕様と実装済みHTMLテンプレート。
> 新規記事作成時は**v1とv2を両方参照**すること。

---

## 1. 出力ルール（必ず守ること）

### 出力順序
記事作成時は以下の順序で**別々に**出力すること。まとめて出力しない。

1. **本文HTML**（H1・リード文を除く）
2. **H1テキスト + リード文HTML**
3. **meta description**
4. 確認後 → **GBP投稿テキスト**

### 文体ルール
- 本文の語尾は必ず**丁寧語（〜です・〜ます）**で統一する
- 以下の表現は使わない：
  - 「〜にある」「〜になる」「〜がある」「〜が欠かせない」（断定・体言止め調）
  - 「〜が必要だ」「〜が重要だ」（偉そうな断定調）
- 正しい例：「〜が大切です」「〜をお勧めします」「〜してください」

---

## 2. ブランドカラーパレット

| 用途 | カラーコード |
|------|------------|
| 本文テキスト | `#2c2c2c` |
| メインネイビー（H2・H3・アイコン背景・FAQのQ背景） | `#1a3a5c` |
| CTAグラデーション起点 | `#0f2340` |
| オーシャン（リンク・ボーダー） | `#2a7ab5` |
| アクセントブルー（H2アンダーライン・H3左ボーダー） | `#4a9fd4` |
| セクションBG薄（著者ボックス・FAQのA背景） | `#f7fbff` |
| 定義ボックスBG | `#e8f4fd` |
| 警告ボックスBG | `#fff8e8` |
| 警告ボーダー | `#f0a500` |
| エラーボックスBG | `#fff0f0` |
| エラーボーダー | `#ffaaaa` |
| 枠線 | `#dce8f0` |
| サブテキスト | `#555555` |
| LINEグリーン | `#06c755` |
| CTAグラデーション | `linear-gradient(135deg, #0f2340 0%, #2a7ab5 100%)` |

---

## 3. 記事全体のラッパー構造

```html
<table style="width: 100%; border-collapse: collapse; font-family: 'Hiragino Kaku Gothic ProN','Meiryo',sans-serif; font-size: 16px; line-height: 1.85; color: #2c2c2c;">
<tbody>
<tr>
<td style="padding: 0;">

  <!-- ここに記事コンテンツを入れる -->

</td>
</tr>
</tbody>
</table>
```

**⚠️ 必須：** 全体を外側tableで囲み、font-family・font-size・colorを一括指定すること。spanを単独で外に出すとBiNDのCSSに上書きされる。

---

## 4. コンポーネント別HTMLスニペット

### 4-1. H2見出し（アイコン付き）

```html
<table style="width: 100%; border-collapse: collapse; border-bottom: 2px solid #4a9fd4; margin-bottom: 24px;">
<tbody>
<tr style="vertical-align: middle;">
<td style="width: 52px; padding: 0 12px 12px 0;">
  <span style="display: inline-block; width: 42px; height: 42px; background: #1a3a5c; border-radius: 50%; text-align: center; line-height: 42px; font-size: 20px;">🤿</span>
</td>
<td style="padding: 0 0 12px;">
  <h2 style="font-size: 21px; color: #1a3a5c; font-weight: bold; margin: 0; line-height: 1.5;">見出しテキスト</h2>
</td>
</tr>
</tbody>
</table>
```

### 4-2. H3見出し

```html
<h3 style="font-size: 17px; color: #1a3a5c; font-weight: bold; border-left: 4px solid #4a9fd4; padding-left: 12px; margin: 0 0 16px; line-height: 1.5;">見出しテキスト</h3>
```

### 4-3. 本文テキスト

```html
<span style="display: block; margin: 0 0 16px; color: #2c2c2c;">本文テキスト（通常段落）</span>
<span style="display: block; margin: 0 0 44px; color: #2c2c2c;">本文テキスト（セクション末尾・大きめ余白）</span>
```

### 4-4. 定義ボックス

```html
<table style="width: 100%; border-collapse: collapse; margin-bottom: 16px;">
<tbody>
<tr>
<td style="padding: 14px 18px; background-color: #e8f4fd; border-left: 4px solid #2a7ab5; border-top: 1px solid #dce8f0; border-bottom: 1px solid #dce8f0; border-right: 1px solid #dce8f0; font-size: 15px; line-height: 1.8; color: #2c2c2c;">
  <strong>用語とは、</strong>定義テキスト。
</td>
</tr>
</tbody>
</table>
```

### 4-5. 警告ボックス

```html
<table style="width: 100%; border-collapse: collapse; background: #fff8e8; border: 1px solid #f0a500; border-radius: 10px; margin-bottom: 32px;">
<tbody>
<tr>
<td style="padding: 18px 22px;">
  <span style="display: block; font-size: 14px; font-weight: bold; color: #b07800; margin: 0 0 8px;">💡 ポイント</span>
  <span style="display: block; font-size: 14.5px; color: #2c2c2c;">警告・アドバイステキスト</span>
</td>
</tr>
</tbody>
</table>
```

### 4-6. データテーブル

```html
<table style="width: 100%; border-collapse: collapse; margin-bottom: 32px; font-size: 14.5px;">
<thead>
<tr>
<th style="background: #1a3a5c; color: #ffffff; padding: 10px 14px; text-align: left; font-weight: bold;">列1</th>
<th style="background: #1a3a5c; color: #ffffff; padding: 10px 14px; text-align: left; font-weight: bold;">列2</th>
</tr>
</thead>
<tbody>
<tr>
<td style="padding: 10px 14px; border: 1px solid #dce8f0; color: #2c2c2c;">データ</td>
<td style="padding: 10px 14px; border: 1px solid #dce8f0; color: #2c2c2c;">データ</td>
</tr>
<tr style="background: #f7fbff;">
<td style="padding: 10px 14px; border: 1px solid #dce8f0; color: #2c2c2c;">データ</td>
<td style="padding: 10px 14px; border: 1px solid #dce8f0; color: #2c2c2c;">データ</td>
</tr>
<tr style="background: #fff8e8;">
<td style="padding: 10px 14px; border: 1px solid #dce8f0; color: #2c2c2c; font-weight: bold;">強調データ</td>
<td style="padding: 10px 14px; border: 1px solid #dce8f0; color: #e05500; font-weight: bold;">強調データ</td>
</tr>
</tbody>
</table>
```

### 4-7. FAQ

```html
<table style="width: 100%; border-collapse: collapse; margin-bottom: 20px;">
<tbody>
<tr>
<td style="padding: 14px 18px; background: #1a3a5c; border-radius: 8px 8px 0 0;">
  <h3 style="font-size: 15.5px; color: #ffffff; font-weight: bold; margin: 0; line-height: 1.6;">Q. 質問テキスト</h3>
</td>
</tr>
<tr>
<td style="padding: 14px 18px; background: #f7fbff; border: 1px solid #dce8f0; border-radius: 0 0 8px 8px;">
  <span style="display: block; font-size: 14px; font-weight: bold; color: #f0a500; margin: 0 0 6px;">A.</span>
  <span style="display: block; font-size: 14.5px; color: #2c2c2c;">回答テキスト</span>
</td>
</tr>
</tbody>
</table>
```

### 4-8. CTAボックス

```html
<table style="width: 100%; border-collapse: collapse; background: linear-gradient(135deg,#0f2340 0%,#2a7ab5 100%); border-radius: 12px; margin-bottom: 44px;">
<tbody>
<tr>
<td style="padding: 28px 26px; text-align: center;">
  <span style="display: block; font-size: 18px; font-weight: bold; color: #ffffff; margin: 0 0 10px;">タイトル</span>
  <span style="display: block; font-size: 14.5px; color: #e8f4fd; margin: 0 0 20px; line-height: 1.85;">サブテキスト</span>
  <table style="margin: 0 auto; border-collapse: collapse;">
  <tbody>
  <tr>
  <td style="padding: 0 8px;">
    <a style="display: inline-block; background: #06c755; color: #ffffff; font-weight: bold; font-size: 15px; padding: 13px 28px; border-radius: 50px; text-decoration: none;" href="https://lin.ee/7wCXQLv">LINEで相談する</a>
  </td>
  <td style="padding: 0 8px;">
    <a style="display: inline-block; background: #ffffff; color: #1a3a5c; font-weight: bold; font-size: 15px; padding: 13px 28px; border-radius: 50px; text-decoration: none;" href="https://ponidiversbali.com/form/fun-booking.html">予約フォームへ</a>
  </td>
  </tr>
  </tbody>
  </table>
</td>
</tr>
</tbody>
</table>
```

### 4-9. 著者ボックス

```html
<table style="width: 100%; border-collapse: collapse; background: #f7fbff; border: 1px solid #dce8f0; border-radius: 12px; margin-bottom: 16px;">
<tbody>
<tr>
<td style="padding: 22px 24px;">
  <span style="display: block; font-size: 13px; font-weight: bold; color: #1a3a5c; margin: 0 0 12px; letter-spacing: 0.08em;">この記事の執筆・監修</span>
  <span style="display: block; font-size: 14.5px; font-weight: bold; color: #2c2c2c; margin: 0 0 10px;">Poni Divers BALI（PADI 5スターダイブセンター認定 S-24583）</span>
  <span style="display: block; font-size: 14px; color: #2c2c2c; margin: 0 0 4px;">■ Yasu ― PADI マスターインストラクター #260159（記事テーマに応じて関連資格を追加）</span>
  <span style="display: block; font-size: 14px; color: #2c2c2c; margin: 0 0 14px;">■ Yuma ― PADI MSDT #312875</span>
  <span style="display: block; font-size: 13.5px; color: #555555;">日本人スタッフが現地の最新情報をもとに執筆しています。</span>
</td>
</tr>
</tbody>
</table>
```

---

## 5. 記事HTMLテンプレート（骨格）

H1・リード文は別エリアに入力するため含まない。

```html
<table style="width: 100%; border-collapse: collapse; font-family: 'Hiragino Kaku Gothic ProN','Meiryo',sans-serif; font-size: 16px; line-height: 1.85; color: #2c2c2c;">
<tbody>
<tr>
<td style="padding: 0;">

<!-- ▼ 用語定義（冒頭に配置） -->
<table style="width: 100%; border-collapse: collapse; border-bottom: 2px solid #4a9fd4; margin-bottom: 24px;">
<tbody><tr style="vertical-align: middle;">
<td style="width: 52px; padding: 0 12px 12px 0;"><span style="display: inline-block; width: 42px; height: 42px; background: #1a3a5c; border-radius: 50%; text-align: center; line-height: 42px; font-size: 20px;">📖</span></td>
<td style="padding: 0 0 12px;"><h2 style="font-size: 21px; color: #1a3a5c; font-weight: bold; margin: 0; line-height: 1.5;">この記事で使う用語</h2></td>
</tr></tbody>
</table>
<!-- 定義ボックス × 必要な数だけ繰り返す -->

<!-- ▼ H2セクション × 3〜5個 -->
<table style="width: 100%; border-collapse: collapse; border-bottom: 2px solid #4a9fd4; margin-bottom: 24px;">
<tbody><tr style="vertical-align: middle;">
<td style="width: 52px; padding: 0 12px 12px 0;"><span style="display: inline-block; width: 42px; height: 42px; background: #1a3a5c; border-radius: 50%; text-align: center; line-height: 42px; font-size: 20px;">🔵</span></td>
<td style="padding: 0 0 12px;"><h2 style="font-size: 21px; color: #1a3a5c; font-weight: bold; margin: 0; line-height: 1.5;">H2見出し</h2></td>
</tr></tbody>
</table>
<span style="display: block; margin: 0 0 16px; color: #2c2c2c;">本文テキスト</span>

<!-- ▼ FAQ -->
<table style="width: 100%; border-collapse: collapse; border-bottom: 2px solid #4a9fd4; margin-bottom: 24px;">
<tbody><tr style="vertical-align: middle;">
<td style="width: 52px; padding: 0 12px 12px 0;"><span style="display: inline-block; width: 42px; height: 42px; background: #1a3a5c; border-radius: 50%; text-align: center; line-height: 42px; font-size: 20px;">❓</span></td>
<td style="padding: 0 0 12px;"><h2 style="font-size: 21px; color: #1a3a5c; font-weight: bold; margin: 0; line-height: 1.5;">よくある質問</h2></td>
</tr></tbody>
</table>
<!-- FAQコンポーネント × 3〜5問 -->

<!-- ▼ CTA -->
<table style="width: 100%; border-collapse: collapse; background: linear-gradient(135deg,#0f2340 0%,#2a7ab5 100%); border-radius: 12px; margin-bottom: 44px;">
<tbody><tr>
<td style="padding: 28px 26px; text-align: center;">
<span style="display: block; font-size: 18px; font-weight: bold; color: #ffffff; margin: 0 0 10px;">タイトル</span>
<span style="display: block; font-size: 14.5px; color: #e8f4fd; margin: 0 0 20px; line-height: 1.85;">日本人スタッフが丁寧にご対応します。</span>
<table style="margin: 0 auto; border-collapse: collapse;"><tbody><tr>
<td style="padding: 0 8px;"><a style="display: inline-block; background: #06c755; color: #ffffff; font-weight: bold; font-size: 15px; padding: 13px 28px; border-radius: 50px; text-decoration: none;" href="https://lin.ee/7wCXQLv">LINEで相談する</a></td>
<td style="padding: 0 8px;"><a style="display: inline-block; background: #ffffff; color: #1a3a5c; font-weight: bold; font-size: 15px; padding: 13px 28px; border-radius: 50px; text-decoration: none;" href="https://ponidiversbali.com/form/fun-booking.html">予約フォームへ</a></td>
</tr></tbody></table>
</td>
</tr></tbody>
</table>

<!-- ▼ 著者ボックス -->
<table style="width: 100%; border-collapse: collapse; background: #f7fbff; border: 1px solid #dce8f0; border-radius: 12px; margin-bottom: 16px;">
<tbody><tr>
<td style="padding: 22px 24px;">
<span style="display: block; font-size: 13px; font-weight: bold; color: #1a3a5c; margin: 0 0 12px; letter-spacing: 0.08em;">この記事の執筆・監修</span>
<span style="display: block; font-size: 14.5px; font-weight: bold; color: #2c2c2c; margin: 0 0 10px;">Poni Divers BALI（PADI 5スターダイブセンター認定 S-24583）</span>
<span style="display: block; font-size: 14px; color: #2c2c2c; margin: 0 0 4px;">■ Yasu ― PADI マスターインストラクター #260159</span>
<span style="display: block; font-size: 14px; color: #2c2c2c; margin: 0 0 14px;">■ Yuma ― PADI MSDT #312875</span>
<span style="display: block; font-size: 13.5px; color: #555555;">日本人スタッフが現地の最新情報をもとに執筆しています。</span>
</td>
</tr></tbody>
</table>

</td>
</tr>
</tbody>
</table>
```

---

## 6. リード文HTMLテンプレート

BiNDのリード文エリアに貼り付ける用。

```html
<table style="width: 100%; border-collapse: collapse; background: #e8f4fd; border-left: 4px solid #2a7ab5; border-radius: 0 10px 10px 0; margin-bottom: 44px;">
<tbody><tr>
<td style="padding: 22px 24px; font-size: 15.5px; line-height: 1.9;">
  <span style="display: block; color: #2c2c2c;">リード文テキスト</span>
</td>
</tr></tbody>
</table>
```

---

## 7. 記事公開前チェックリスト

### 出力順序
- [ ] 本文HTML（H1・リード文なし）を先に出したか
- [ ] H1テキスト＋リード文HTMLを次に出したか
- [ ] meta descriptionを次に出したか
- [ ] GBP投稿テキストを最後に出したか

### 文体
- [ ] 語尾がすべて「〜です・〜ます」調になっているか
- [ ] 「〜にある」「〜になる」「〜がある」「〜が欠かせない」が含まれていないか

### HTML構造
- [ ] 全体が外側tableで囲まれているか
- [ ] spanがすべてtd内に入っているか
- [ ] `<div>`・`<p>`が0個であること
- [ ] `display:flex`が0個であること

### デザイン
- [ ] H2にアイコン丸＋border-bottom:2px solid #4a9fd4が使われているか
- [ ] H3にborder-left:4px solid #4a9fd4が使われているか
- [ ] 定義ボックスにbg:#e8f4fd / border-left:#2a7ab5が使われているか
- [ ] FAQがQ青背景・A薄青背景の2段構造になっているか
- [ ] CTAがグラデーション背景・ボタンborder-radius:50pxになっているか
- [ ] 著者ボックスがbg:#f7fbff / border:#dce8f0になっているか
