# 開発ガイド

## 開発環境のセットアップ

### 1. Chrome拡張機能の読み込み

1. Chromeブラウザで `chrome://extensions/` を開く
2. 右上の「デベロッパーモード」をONにする
3. 「パッケージ化されていない拡張機能を読み込む」をクリック
4. このフォルダ（`ufret-adblock`）を選択

### 2. 動作確認手順

#### 基本的な動作確認

1. U-FRETサイト（または広告が表示されるサイト）を開く
2. ブラウザの開発者ツールを開く（F12 または 右クリック → 検証）
3. Consoleタブで以下のログを確認：
   - `[U-FRET Ad Blocker] デバッグモード有効`
   - `[U-FRET Ad Blocker] X個の要素を削除しました`

#### デバッグコマンド

Consoleで以下のコマンドが使用できます：

```javascript
// 現在のページで検出された広告要素を一覧表示
ufretAdBlockerDebug.listAds()

// 手動で広告削除を実行
ufretAdBlockerDebug.removeAds()

// 削除対象のセレクタを確認
ufretAdBlockerDebug.selectors
```

### 3. ファイル変更時の再読み込み

コードを変更した場合は：

1. `chrome://extensions/` ページで拡張機能の「再読み込み」ボタンをクリック
2. または、対象ページをリロード（F5）

### 4. Content Scriptのデバッグ

1. 広告が表示されるページを開く
2. ページ上で右クリック → 「検証」を選択
3. Consoleタブでログを確認
4. Elementsタブで削除された要素が存在しないことを確認

### 5. よくある問題と対処法

#### 広告が削除されない場合

1. Consoleでエラーログを確認
2. `ufretAdBlockerDebug.listAds()` で要素が検出されているか確認
3. セレクタが正しいか確認（Elementsタブで要素を検証）

#### 拡張機能が読み込まれない場合

1. `manifest.json` の構文エラーを確認
2. Chrome拡張機能のページでエラーメッセージを確認
3. Consoleでエラーログを確認

### 6. パフォーマンス確認

- 開発者ツールのPerformanceタブでパフォーマンスを測定
- 定期的なチェック（2秒間隔）がページに影響を与えていないか確認

### 7. 本番環境への移行

本番環境では `content.js` の `DEBUG_MODE` を `false` に設定してください：

```javascript
const DEBUG_MODE = false;
```

## テスト手順

1. U-FRETサイトを開く
2. 広告要素が表示されることを確認
3. 拡張機能を有効化
4. ページをリロード
5. 広告要素が削除されていることを確認
6. Consoleで削除ログを確認

