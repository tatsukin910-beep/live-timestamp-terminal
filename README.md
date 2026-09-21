# Live Timestamp Terminal

JST（Asia/Tokyo, UTC+09:00）固定のオフライン・タイムスタンプコピーツール。  
PCブラウザでの利用を前提に、時刻計算・UI・ショートカットを厳密化している。

リポジトリ: https://github.com/tatsukin910-beep/live-timestamp-terminal

## 仕様（PC / JST STRICT）

- 表示時計は **24時間制**（`HH:MM:SS`）。端末のタイムゾーン設定は使わない。
- 時刻パーツは `Intl.DateTimeFormat` + `timeZone: "Asia/Tokyo"` + `hourCycle: "h23"`。
- Unix のみ UTC epoch 秒（絶対時刻）。壁時計ではない。
- フォーマット選択の option 文言は **固定**。毎秒更新するのはプレビュー行のみ。  
  （旧実装は option を毎秒書き換え、PC でドロップダウン操作中に選択肢が崩れる）
- 選択フォーマットは `localStorage` キー `ltt.format.v2` に保存。
- コピー対象はボタン押下（またはショートカット）**瞬間**の JST。

## ショートカット

| キー | 動作 |
| --- | --- |
| `C` | 現在時刻をキャプチャしてコピー |
| `Enter` | 同上（SELECT 上では発火しない） |
| `Esc` | LAST CAPTURED をクリア |

## 対応フォーマット

- `custom24` — `21-Sep-2026 — 19:00:00 (JST, UTC+09:00)`（既定）
- `custom` — 12時間制 + AM/PM
- `long` / `us`
- `iso` — `YYYY-MM-DDTHH:MM:SS+09:00`
- `datetime` — `YYYY-MM-DD HH:MM:SS JST`
- `japanese` — `YYYY年MM月DD日(曜) HH時MM分SS秒`
- `unix` — epoch seconds

## 使い方（PC）

1. GitHub Pages で開く、またはローカルで静的配信する。
2. `file://` では Clipboard API と Service Worker が制限される。コピーはフォールバックで動く場合があるが、確認は http(s) で行う。
3. フォーマットを選び、「今の時刻をコピー」または `C`。

ローカル確認例:

```bash
python -m http.server 8080
```

`http://127.0.0.1:8080/` を開く。

## 修正内容（この版）

- メイン時計を 12h+AM/PM から 24h に変更
- option テキストのライブ上書きを廃止（PC の select 安定性）
- `hourCycle: "h23"` で hour=24 を抑制
- タブ復帰時に時計を再同期
- 同一秒の重複描画を抑制
- PC幅（720px）、等幅数字、キーボード操作
- `user-select: none` を廃止（PCで文字列を選べるようにした）
- Service Worker キャッシュ名を `live-timestamp-v2` に更新

## 技術

- 単一 HTML + 小さな `sw.js` / `manifest.json`
- 外部 CDN・解析なし

## License

MIT
