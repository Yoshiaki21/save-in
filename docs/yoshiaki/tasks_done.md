# 完了タスク記録

## 記録フォーマット
完了タスクは以下の形式で追記すること。
`docs/yoshiaki/tasks.md` から該当タスクを削除し、`MY_CLAUDE.md` のタスク状況テーブルを ✅ に更新すること。

```
---

## タスク[番号]: [タイトル]

- **完了日**: YYYY-MM-DD
- **動作確認**: ✅済み / ⬜未確認
- **新規ファイル**:
  - `パス/ファイル名` : 用途
- **修正ファイル**:
  - `パス/ファイル名` : 変更内容を一言で
- **変更内容**:
  - 箇条書きで何をしたか
- **備考**: ハマった点・注意事項（なければ省略）
```

<!-- 以下に完了タスクを追記 -->

---

## タスク1: _locales/ja/messages.json 作成（全キー翻訳）

- **完了日**: 2026-06-03
- **動作確認**: ⬜未確認
- **新規ファイル**:
  - `_locales/ja/messages.json` : 全キー（80件）の日本語訳
- **変更内容**:
  - `_locales/en/messages.json` の全キーを日本語に翻訳して `_locales/ja/messages.json` を新規作成
- **備考**: インストール後に日本語が表示されない場合は Firefox の UI 言語設定を確認すること。
  `__MSG_xxx__` の置換は `src/options/vendor/l10n/l10n.js` が `chrome.i18n.getMessage()` を呼び出して行う。
  この API は Firefox の UI 言語（`about:preferences` → 言語、または `about:config` の `intl.locale.requested`）が `ja` になっていないと
  `_locales/ja/messages.json` を使わない。英語 UI のまま日本語化したい場合は別途対応が必要。

---

## タスク2: オプションページのi18n対応確認・修正

- **完了日**: 2026-06-03
- **動作確認**: ⬜未確認
- **修正ファイル**:
  - `src/options/options.js` : line 72 の "no matches" ハードコードを `browser.i18n.getMessage` に変更
- **変更内容**:
  - `src/options/` の全HTMLファイルを走査し、`__MSG_xxx__` 未対応テキストを一覧化
  - `options.html`: ほぼ全UIラベルが対応済み。既存キー `o_lRoutingNoMatches` を JS側でも使うよう `options.js:72` を修正
  - 対応不可箇所（`en/` 編集禁止のため）: "History"・"Delete history"ボタン・エラー通知の初期テキスト・`clauselist.html`・`variablelist.html` の全文

---

## 不具合調査: オプションページが表示されない

- **発生日**: 2026-06-03
- **動作確認**: ⬜未確認
- **原因**:
  `manifest.json` の `options_ui` に `"open_in_tab": true` が指定されていなかった。
  この設定がない場合、Firefox はオプションページを新しいタブで開かず `about:addons`（拡張機能管理ページ）内にインライン表示しようとする。
  ユーザーには `about:addons` が裏タブで開いているだけに見え「オプションが表示されない」と感じる。
- **修正ファイル**:
  - `manifest.json` : `options_ui` に `"open_in_tab": true` を追加
- **変更内容**:
  - `manifest.json` の `options_ui` に `"open_in_tab": true` を追加し、オプションページを独立した新タブで開くように変更
- **備考**:
  - `browser.runtime.openOptionsPage()` は正常に動作しており、コードレベルのバグはなし
  - `open_in_tab: true` は Firefox 57+ でサポート済み
  - permissions の変更ではないため MY_CLAUDE.md のルール範囲内
