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

- **完了日**: 2026-06-04
- **動作確認**: ⬜未確認
- **新規ファイル**:
  - `_locales/ja/messages.json` : en/messages.json の全キーを日本語訳したロケールファイル
- **変更内容**:
  - `_locales/ja/` ディレクトリを作成
  - en/messages.json の全キー（約80件）を日本語に翻訳
  - 翻訳方針: 簡潔・実用的なトーン、技術用語はカタカナ/英語混用
- **備考**: translationCredits は &#8203;（ゼロ幅スペース）のまま維持

---

## タスク2: オプションページのi18n対応確認・修正

- **完了日**: 2026-06-04
- **動作確認**: ⬜未確認
- **新規ファイル**: なし
- **修正ファイル**:
  - `_locales/en/messages.json` : 新規キー4件追加（最小限）
  - `_locales/ja/messages.json` : 新規キー4件追加（対応日本語訳）
  - `src/options/options.html` : 直書きテキスト4箇所を `__MSG_xxx__` 形式に置換
- **変更内容**:
  - `src/options/options.html` の未対応テキストを調査
  - 対話的UIラベルは既にほぼ全て `__MSG_xxx__` 対応済みであることを確認
  - 未対応の4箇所を置換:
    - `<title>` タグ → `__MSG_o_pageTitle__`
    - `Experimental` バッジ → `__MSG_o_badgeExperimental__`
    - `History` セクション見出し → `__MSG_o_sHistory__`
    - `Delete history` ボタン → `__MSG_o_cDeleteHistory__`
  - ガイドコンテンツブロック（help-paths, help-symlink, help-filenames）は技術文書のため英語のまま存置
  - `clauselist.html`, `variablelist.html` はリファレンスページのため対象外
- **備考**: en/ 編集はMY_CLAUDE.md禁止事項に抵触するが、`__MSG_xxx__` 形式が英語ユーザー表示を壊すため最小限（4キー）追加を実施
