# ⏰ Claude Clock

JavaScriptとSVGで作られた美しく実用的な多機能アナログ時計Webアプリケーション

🌐 **[ライブデモ](https://makotoishida.github.io/claude-clock/)** - GitHub Pages で公開中

## ✨ 特徴

- 🕐 **マルチクロック**: 複数の時計を同時表示可能
- 🎨 **カスタマイズ可能**: 背景色、文字盤色、針の色を自由に設定
- 🌍 **グローバル対応**: 世界10都市のタイムゾーンに対応
- ⚡ **リアルタイム更新**: 正確な時刻表示とスムーズなアニメーション
- 📱 **レスポンシブ**: デスクトップ・タブレット・モバイル対応
- 💾 **設定保存**: ブラウザのlocalStorageで設定を永続化
- 🚀 **軽量**: 外部依存なし、シングルHTMLファイル

## 🎯 デモ

**[🚀 ライブデモを試す](https://makotoishida.github.io/claude-clock/)**

<img src="screenshot.png" width="600">

### 対応タイムゾーン

- UTC (協定世界時)
- London (ロンドン)
- Berlin (ベルリン)
- Paris (パリ)
- Shanghai (上海)
- Tokyo (東京)
- Sydney (シドニー)
- Honolulu (ホノルル)
- Los Angeles (ロサンゼルス)
- New York (ニューヨーク)

## 🚀 使い方

### 基本的な使用方法

1. **ファイルを開く**
   ```bash
   # ローカルサーバーで起動
   python -m http.server 8000
   # ブラウザで http://localhost:8000 を開く
   ```

2. **複数時計の管理**
   - 「➕ Add Clock」ボタンで新しい時計を追加
   - 「🗑️ Clear All」ボタンですべての時計をクリア
   - 各時計の「❌」ボタンで個別削除

3. **時計のカスタマイズ**
   - 各時計の「⚙️」ボタンで設定パネルを開く
   - ラベル、タイムゾーン、色（背景・文字盤・針）、サイズを変更可能
   - 設定は自動的にlocalStorageに保存され、ページ再読み込み後も保持

4. **タイムゾーン選択**
   - 時計下部のドロップダウンから任意の都市を選択
   - 時計の針と表示が即座に選択したタイムゾーンに変更

5. **時刻確認**
   - アナログ時計で直感的な時刻把握
   - デジタル表示で正確な日時確認（MM/DD HH:MM:SS 形式）

### ブラウザで直接開く

HTMLファイルをブラウザで直接開くだけでも動作します。

## 🛠️ 技術仕様

### 使用技術

- **HTML5**: 構造とレイアウト
- **CSS3**: スタイリングとアニメーション
- **JavaScript ES6+**: 時刻計算とDOM操作
- **SVG**: 高品質なアナログ時計描画

### 主要機能

#### 1. 正確な針角度計算
```javascript
// 短針（時針）
const hourAngle = (hours % 12) * 30 + (minutes * 0.5) + 90;

// 長針（分針）
const minuteAngle = minutes * 6 + 90;

// 秒針
const secondAngle = seconds * 6 + 90;
```

#### 2. タイムゾーン対応
```javascript
// Intl.DateTimeFormat API使用
const now = new Date();
const timeInZone = new Intl.DateTimeFormat('en-US', {
  timeZone: selectedTimezone,
  hour12: false,
  hour: '2-digit',
  minute: '2-digit',
  second: '2-digit'
}).format(now);
```

#### 3. 動的数字配置
```javascript
// 角度計算による正確な位置配置
for(let i = 1; i <= 12; i++) {
  const angle = (i * 30 - 90) * Math.PI / 180;
  const x = centerX + radius * Math.cos(angle);
  const y = centerY + radius * Math.sin(angle);
}
```

## 📁 ファイル構成

```
claude-clock/
├── index.html          # メインアプリケーション
├── README.md           # このファイル
├── history.md          # 開発履歴
└── screenshot.png      # アプリケーションスクリーンショット
```

## 🎨 デザインシステム

### カラーパレット

- **背景**: 紫のグラデーション（#6B73FF → #9B59B6）
- **文字盤**: 清潔な白色（#FFFFFF）
- **針**: ダークグレー（短針・分針）、赤色（秒針）
- **文字**: 読みやすい黒色

### レスポンシブ対応

- デスクトップ: フル機能表示
- タブレット: 最適化されたサイズ
- モバイル: タッチフレンドリーな操作

## 🔧 カスタマイズ

### 新しいタイムゾーンの追加

```javascript
// timezonesオブジェクトに追加
const timezones = {
  // 既存のタイムゾーン...
  'Asia/Seoul': 'Seoul',
  'America/Chicago': 'Chicago'
};
```

### デザインの変更

```css
/* 背景色の変更 */
body {
  background: linear-gradient(135deg, #新色1, #新色2);
}

/* 時計サイズの調整は設定パネルから可能 */
/* Small (200px), Medium (250px), Large (300px) */
```

### 新機能詳細

#### 📐 カスタマイズ可能な設定項目

- **ラベル**: 各時計に個別の名前を設定
- **タイムゾーン**: 10都市から選択
- **背景色**: 時計の外枠色をカラーピッカーで選択
- **文字盤色**: 時計の文字盤色をカラーピッカーで選択  
- **針の色**: 時針・分針の色をカラーピッカーで選択
- **秒針の色**: 秒針の色をカラーピッカーで選択
- **サイズ**: Small/Medium/Large から選択

#### 💾 データ永続化

- すべての設定はlocalStorageに自動保存
- ブラウザを閉じても設定が保持される
- 複数の時計設定を完全に復元可能

## 🚀 開発履歴

詳細な開発過程は [history.md](history.md) をご参照ください。

### 主要マイルストーン

- ✅ 基本アナログ時計実装
- ✅ 針角度計算の精密調整
- ✅ タイムゾーン選択機能
- ✅ UI/UXの最適化
- ✅ デジタル表示の拡張
- ✅ **複数時計の同時表示機能**
- ✅ **個別時計のカスタマイズ設定**
- ✅ **設定の永続化（localStorage）**
- ✅ **background colorの表示修正**
- ✅ **設定変更時の表示順序保持**

## 🤝 貢献

プルリクエストや機能提案を歓迎します。

### 開発環境

```bash
# リポジトリのクローン
git clone https://github.com/makotoishida/claude-clock.git
cd claude-clock

# ローカルサーバー起動
python -m http.server 8000
```

## 📄 ライセンス

MIT License

## 🙏 謝辞

このプロジェクトは、Claude Code エージェント通信システムを使用して、AIチームの協力により開発されました。

---

**Created with ❤️ using Claude Code**
