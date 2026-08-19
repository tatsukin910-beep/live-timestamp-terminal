# Live Timestamp Terminal

**JST固定・完全オフライン対応のライブタイムスタンプコピーツール**

リアルタイムでJST（日本標準時）を表示し、複数のフォーマットでタイムスタンプをワンタップコピーできるPWA（Progressive Web App）です。

## 特徴

- 🌐 **完全オフライン動作**（Service Worker + Cache）
- 🇯🇵 **JST厳密固定**（端末のタイムゾーン設定に依存しない）
- 📋 **ワンタップコピー**（複数フォーマット対応）
- 📱 **ホーム画面追加対応**（iOS / Android PWA）
- 🔒 **外部サービスなし**（プライバシー重視）

## 対応フォーマット

- Custom 12h / 24h
- Long English
- US Style
- ISO 8601
- DateTime
- Japanese（年月日・時分秒）
- Unix Timestamp

## 使い方

1. このリポジトリを GitHub Pages などで公開するか、ローカルで `index.html` を開く
2. ブラウザで「ホーム画面に追加」を選択
3. アプリのように起動して使用

### iOS (Safari)

1. 共有ボタンをタップ
2. 「ホーム画面に追加」を選択
3. 追加

### Android (Chrome)

1. メニュー → 「ホーム画面に追加」または「アプリをインストール」

## 技術

- Pure HTML / CSS / Vanilla JS
- Service Worker for offline caching
- Web App Manifest
- Intl.DateTimeFormat による厳密な JST 計算

## License

MIT
