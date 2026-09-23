# Live Timestamp Terminal

JST（Asia/Tokyo, UTC+09:00）固定のオフライン・タイムスタンプコピーツール。  
PCブラウザでの利用を前提に、時刻計算・UI・ショートカットを厳密化している。

- リポジトリ: https://github.com/tatsukin910-beep/live-timestamp-terminal
- Pages: https://tatsukin910-beep.github.io/live-timestamp-terminal/

## GitHub Actions 自動デプロイ

`main` への push、または Actions 画面の Run workflow で GitHub Pages に静的サイトを配信する。

ワークフロー: `.github/workflows/deploy-pages.yml`

### 最初だけ手動で確認する項目

1. リポジトリ → **Settings** → **Pages**
2. **Source** を **GitHub Actions** にする（Deploy from a branch のままだと Actions 配信が失敗する）
3. **Actions** タブで `Deploy GitHub Pages` が緑になることを確認
4. 公開URL: https://tatsukin910-beep.github.io/live-timestamp-terminal/

キャッシュされた古い `sw.js` が残っている場合はブラウザでスーパーリロード（Ctrl+F5）する。

## 仕様（PC / JST STRICT）

- 表示時計は **24時間制**（`HH:MM:SS`）。端末のタイムゾーン設定は使わない。
- 時刻パーツは `Intl.DateTimeFormat` + `timeZone: "Asia/Tokyo"` + `hourCycle: "h23"`。
- Unix のみ UTC epoch 秒（絶対時刻）。壁時計ではない。
- フォーマット選択の option 文言は **固定**。毎秒更新するのはプレビュー行のみ。
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
2. `file://` では Clipboard API と Service Worker が制限される。確認は http(s) で行う。
3. フォーマットを選び、「今の時刻をコピー」または `C`。

ローカル確認例:

```bash
python -m http.server 8080
```

`http://127.0.0.1:8080/` を開く。

## License

MIT
