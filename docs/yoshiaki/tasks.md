## タスク3: クリック保存(Click to Save)が最新Firefoxで機能しない問題の修正

### 概要
オプションの「クリックして保存」(`contentClickToSave`)が、最新Firefox + 近年のWebサイト構造で
実質機能していない。クリック検出ロジックを堅牢化して動作するように修正する。
対象は `src/content/content.js` の `if (options.contentClickToSave) { ... }` ブロック。

### 例外許可（重要）
- 本タスクに限り **`src/content/content.js`（フォーク元ファイル）の変更を許可する**。
  MY_CLAUDE.md「フォーク元ファイルは極力変更しない」の例外として扱うこと。
- 完了時、tasks_done.md の備考にフォーク元ファイル変更の例外である旨を記録すること。

### 原因（仮説）
1. 修飾キーの押下状態を keydown/keyup で追跡しているが、Altメニュー起動やフォーカス移動で
   状態がズレ、mousedown時に「押下中」と認識されないことがある。
2. `e.target.currentSrc || e.target.src` のみで取得しているため、画像が透明オーバーレイや
   ラッパ要素で覆われているサイト(X/pixiv/Instagram等)では `src` を拾えず無言で失敗する。
3. number入力(`contentClickToSaveCombo`)が文字列として保存され得る。

### 手順
1. **再現・切り分け（先に実施）**
   - `src/content/content.js` の mousedown ハンドラ冒頭に一時的なデバッグログを入れる。
   - `yarn d`（Windowsなら `yarn d:win:stable`）で開発用Firefoxを起動。
   - オプションで「クリックして保存」をON→対象ページをリロード。
   - `about:debugging` → 当拡張の「調査」(content側コンソール)で、
     ① mousedown が発火するか ② `e.altKey` が true か ③ メディア要素を取得できているか を確認。
   - 切り分け結果を tasks_done.md の備考にメモする。
2. **本修正の適用**
   - `if (options.contentClickToSave) { ... }` ブロックを、別途共有する修正版コードで丸ごと置換。
   - 変更点: (a) 修飾キー判定をマウスイベントのフラグ直読み(e.altKey等)に変更し、
     標準修飾キー以外のみ keydown/keyup 追跡を使用。
     (b) `closest` + `document.elementsFromPoint` でメディア要素を解決し、オーバーレイ対応。
     (c) combo値を `Number` 化。
   - デバッグログは削除する。
3. **検証**
   - `yarn lint`（web-ext lint + eslint）が通ること。
   - `yarn test`（jest）が通ること。
   - `yarn d` で実機確認: 通常の `<img>`、およびオーバーレイで覆われた画像(例: X/pixiv)で
     Alt+左クリック保存が動作すること。**この実機確認は人間が行う**。
   - 修飾キーをCtrl(17)に変更した場合も動作することを確認（保存後リロード必須）。
4. **ビルド（任意）**
   - 配布用に確認する場合は `yarn build`。

### 注意事項
- `manifest.json` の permissions は変更しない（MY_CLAUDE.md 禁止事項）。
- iframe内画像への対応(`all_frames: true`)は manifest 変更を伴うため本タスクの対象外。
  必要なら別タスクとして切り出す。
- `e.target.closest` が undefined になり得るケース(target が document 等)はガード済みであること。

### Claude Codeへの指示文（例）
```
docs/yoshiaki/MY_CLAUDE.md を読んでから作業を開始してください。
docs/yoshiaki/tasks.md のタスク3を実装してください。
本タスクでは src/content/content.js の変更を明示的に許可します。
まず手順1の切り分けを行い、結果を報告してから手順2の修正を適用してください。
```
