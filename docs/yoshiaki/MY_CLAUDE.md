# save-in - よしあき個人設定

## 作業ファイル
- 未着手・進行中: `docs/yoshiaki/tasks.md`
- 完了記録: `docs/yoshiaki/tasks_done.md`（なければ新規作成）
- 記録フォーマットは `docs/yoshiaki/tasks_done.md` 冒頭を参照

## このプロジェクトのルール
- フォーク元ファイルは極力変更しない
- `CLAUDE.md`（フォーク元）は編集しない
- `_locales/en/` は編集しない（上流との差分最小化）
- コミットには [yoshiaki] プレフィックスをつける
  例: `[yoshiaki] Add Japanese locale for options page`
- manifest.json の permissions は変更しない

## 技術情報
- 依存インストール: `yarn install`
- 開発用Firefox起動: `yarn d`
- テスト実行: `yarn test`
- ビルド: `yarn build`
- 動作確認: Firefoxで `about:debugging` → 「一時的なアドオンを読み込む」→ `manifest.json` を選択

## 日本語化の方針
- `_locales/ja/messages.json` を正とする
- HTMLへの直書きテキストは `__MSG_xxx__` 形式に置き換える
- 翻訳トーン: 簡潔・実用的（敬語不要）
- 技術用語はカタカナ/英語混用OK

## 禁止事項
- `CLAUDE.md`（フォーク元）は編集しない
- `_locales/en/` は編集しない
- `manifest.json` の permissions は変更しない
- `yarn.lock` は手動編集しない

## タスク状況
| # | タイトル | 状態 |
|---|---------|------|
| 1 | _locales/ja/messages.json 作成（全キー翻訳） | ⬜未着手 |
| 2 | オプションページHTML直書き箇所のi18n対応確認・修正 | ⬜未着手 |
<!-- ⬜未着手 / 🔄進行中 / ✅完了 -->
