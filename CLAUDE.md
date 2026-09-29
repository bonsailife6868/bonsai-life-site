# 盆栽ライフ（BONSAI LIFE）ホームページ

盆栽ライフのWebサイト。ビルド不要の静的HTML。

## 構成

- `index.html` — トップページ（CSS・JSは全部この中。PC／スマホ対応）
- `assets/` — 写真（園内で撮影したもの。JPG）
- `design/design-system.md` — デザインのルール（色・文字・形・写真・言葉づかい）
- `design/tokens.json` — 色・文字サイズ・余白などの値
- `design/canvas/*.dc.html` — Claudeのデザインキャンバスのデータ（参考用。画像は `/_blob/...` を指しているので、ブラウザで直接は開けない）

## 編集のルール

- 色・フォント・余白は `design/design-system.md` と `design/tokens.json` に合わせる。`index.html` の `:root` にある CSS 変数（`--paper` `--ink` `--moss` `--muted` `--line` `--orange`）を使う。
- フォントは Google Fonts の Noto Serif JP（見出し・読みもの）と Zen Kaku Gothic New（本文・ナビ）。
- 角は丸めない。アクセントの柿渋色（`--orange`）は英字キッカーとタグだけに使う。
- 下層ページは `index.html` と同じヘッダー・フッターで、ファイルを分けて作る（例：`school.html`、`gallery.html`）。
- 写真を追加するときは `assets/` に Web 用の JPG（長辺 1600〜2200px 程度）で置く。
- 動画の再生ボタンと note の最新記事カードはまだ仮の枠。

## デザインキャンバスとの関係

デザインは Claude のデザインキャンバスで決め、このフォルダのコードに反映する。自動では同期しない。

- デザインキャンバス（見た目の正本）：https://claude.ai/artifact/99tZ9ipYRqBfqccUMbxamn
  - `Main.dc.html` = トップページ（PC・幅1440px）、`Mobile.dc.html` = トップページ（スマホ・幅390px）
  - 下層ページもここに追加していく
- デザインシステム（色・文字・写真のルール）：https://claude.ai/code/artifact/97a487fa-f753-4d79-9ce9-74e0379839c4
- 以前公開したトップページのプレビュー（古い版・参考）：https://claude.ai/artifact/K3gHDJyJAoHEZxr6A2Jnij

### 担当の分け方

- 見た目（レイアウト・色・写真・文章）→ キャンバスで変える
- 動き・実装（メニュー、動画、note連携、公開準備など）→ このフォルダで変える
- 同じ部分を両方で同時に変えない（片方が上書きされる）

### キャンバスの変更をコードに反映するとき

1. キャンバスのURLから最新の `.dc.html` を読む（読めない環境なら、ユーザーに Cowork で「キャンバスの変更を projectHTML に反映して」と頼んでもらう）
2. `design/canvas/` の古いコピーと比べて、変わった部分だけを `index.html`（下層ページは各HTML）に反映する
3. `.dc.html` はインラインスタイルで書かれているが、`index.html` ではクラスと `:root` の CSS 変数を使う形を保つ。PC版とスマホ版の差はメディアクエリ（960px / 760px）で書く
4. 画像は `/_blob/...` ではなく `assets/` のファイルを使う。新しい写真はユーザーに元ファイルをもらって `assets/` に置く
5. 反映後、`design/canvas/` のコピーを最新に更新する

### コードで見た目を変えたとき

キャンバスには自動で戻らない。ユーザーに Cowork で「projectHTML の変更をキャンバスに反映して」と頼んでもらう。
