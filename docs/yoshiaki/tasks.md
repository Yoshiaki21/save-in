# save-in 作業指示書

<!-- 未着手・進行中のタスクをここに記載する -->
<!-- 完了したタスクは docs/yoshiaki/tasks_done.md に移動すること -->

---

## タスク1: _locales/ja/messages.json 作成（全キー翻訳）

### 概要
`_locales/en/messages.json` を参照し、全キーを日本語に翻訳した `_locales/ja/messages.json` を新規作成する。

### 手順
1. `_locales/en/messages.json` の全キーを確認する
2. `_locales/ja/` ディレクトリを作成する
3. `_locales/ja/messages.json` を新規作成し、全メッセージを日本語に翻訳する

### 翻訳方針
- 簡潔・実用的なトーン（敬語不要）
- 技術用語はカタカナ/英語混用OK
- 例:
  - "Save In…" → "Save In…"（固有名詞はそのまま）
  - "Last used" → "最後に使った場所"
  - "Options" → "オプション"
  - "Download directory" → "ダウンロード先"

---

## タスク2: オプションページのi18n対応確認・修正

### 概要
オプションページ（`src/options/` 配下）のHTMLに直書きされたテキストを確認し、
`__MSG_xxx__` 形式に置き換えてi18n対応する。

### 手順
1. `src/options/` 配下のHTMLファイルを全走査する
2. `__MSG_xxx__` 形式になっていない日本語化対象テキストを一覧化する
3. 対応する `message` キーを `_locales/en/messages.json` および `_locales/ja/messages.json` に追加する
4. HTMLの直書きテキストを `__MSG_xxx__` 形式に置き換える

### 注意事項
- `_locales/en/messages.json` に新規キーを追加する場合は最小限にとどめる
- 既存キーで代用できる場合は既存キーを使う

---

## Claude Codeへの指示

```
docs/yoshiaki/MY_CLAUDE.md を読んでから作業を開始してください。
docs/yoshiaki/tasks.md のタスク1→タスク2の順に実装してください。

```
