# bunchoniki Retro - iPhone レトロゲーム合法プレイ情報サイト

iPhone でレトロゲーム（GB/GBC/GBA/NES/SNES/N64/NDS/Genesis）を**合法的に**楽しむ方法を日本語で提供する Web サイト。**Delta エミュレータ × GB Operator × 著作権法第30条**の統合解説を最大の差別化ポイントとして展開。

## 姉妹サイト

サイドローディング・AltStore PAL・スマホ新法解説は **bunchoniki Store**（https://altstore-jp.bunchoniki.com / repo: `sazanamiNiki/altStore`）で扱います。両サイトは独立した GitHub repo として運用し、相互リンクで送客します。

## 概要

- **目的**: iPhone でレトロゲームを合法的に楽しむためのフルフロー解説
- **対象ユーザー**: 押し入れにカートリッジを眠らせている人、iPhone でレトロゲームを遊びたい人
- **差別化ポイント（他サイトにない独自コンテンツ）**:
  - **Delta+GB Operator+著作権法第30条 の統合解説** — カートリッジ→ROM吸い出し→Delta→iPhoneの合法フルフローを法的根拠付きで解説する日本語サイトは他にない
  - **エミュレータ法律早見表** — GB系（合法）vs Switch系（違法リスク）の技術的・法的整理
  - **homebrew ゲーム特集** — itch.io で配布される合法 ROM の紹介
- **主なコンテンツ**:
  - Delta エミュレータ完全ガイド
  - GB Operator によるカートリッジからの合法吸い出し
  - 著作権法第30条と不正競争防止法の整理
  - homebrew 無料ゲーム特集

## SEO戦略

- **IndexNow**: デプロイ後に `npm run indexnow` で Bing/Yandex 等に即時通知
- **サイトマップ**: 初期は全主要記事を含める（少数なので絞り込み不要）
- **永続コンテンツ重視**: ニュース駆動ではなく、レトロゲーム×法律という普遍的需要に応える

## プロジェクト構成

詳細は @.claude/rules/project-map.md を参照。

## 編集ルール

### デザイン・レスポンシブ規約

UI・レスポンシブ設計のルールは `./.claude/rules/design.md` を参照してください。

- **モバイルファースト**: padding/margin/font-size は必ず `sm:` プレフィックス付きのレスポンシブ値を併記
- 固定値ベタ書き（`p-8`, `text-4xl` 等）は禁止
- `border-gray-100` は白背景で視認不可のため禁止。`border-gray-200` 以上を使用
- 見出しの flex 配置は `items-center` ではなく `items-start` + アイコンに `flex-shrink-0`

### 記事スタイルガイド

記事ページ（`src/pages/articles/*.mdx`）の編集・作成ルールは `./.claude/rules/articles_style_guide.md` を参照してください。

主なポイント：
- Tailwind CSS ベースの統一デザイン
- **アイコン**: 原則として絵文字ではなく Material Symbols Outlined（MUI）を色付きで使用
- 青・黄・緑のカラースキーム（retrogame はインディゴをアクセントに）
- 記事は MDX 形式で記述し、`src/components/` の Astro コンポーネントを活用

### 姉妹サイトとの相互リンク

- 同サイト内の記事リンク: 相対 URL（`/articles/foo/`）
- 姉妹サイト bunchoniki Store へのリンク: 絶対 URL（`https://altstore-jp.bunchoniki.com/articles/foo/`）+ `target="_blank" rel="noopener"`

## 技術スタック

- Astro 4.16 + MDX（静的サイト生成）
- Tailwind CSS 3.4（`@astrojs/tailwind`）
- TypeScript
- Material Symbols Outlined（アイコン）

## 開発コマンド

```bash
npm install       # 初回のみ
npm run dev       # 開発サーバー
npm run build     # 本番ビルド
npm run preview   # ビルド結果プレビュー
npm run indexnow  # IndexNow ping（デプロイ後）
```

## デプロイ

`master` ブランチへの push で GitHub Actions が自動ビルド・デプロイします（→ retrogame.bunchoniki.com）。`develop` ブランチは `/dev` プレビュー。

## デプロイフロー

ユーザーから「作業内容を反映してください」と指示された場合：

1. **変更をコミット**（`Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>` を含める）
2. **developブランチにマージ**: `git checkout develop && git merge master && git push origin develop`
3. **PR作成・マージ**: `gh pr create --base master --head develop` → `gh pr merge [PR番号] --merge`
4. **master同期**: `git checkout master && git pull origin master`
5. **IndexNow ping**: `npm run indexnow`

途中で確認を求めずに自動実行してください。
