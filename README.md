# 🎴 UNO風カードゲーム

本格的なUNOのルールを実装したブラウザベースのマルチプレイヤーカードゲームです。最大8人まで対戦可能で、標準UNOの全ての主要機能を備えています。

![UNO Game Screenshot](https://img.shields.io/badge/Game-UNO--like-brightgreen)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)

## ✨ 主な機能

### 🃏 完全なカードデッキ (108枚)
- **数字カード**: 各色0-9 (76枚)
- **アクションカード**: スキップ、リバース、ドロー2 (24枚)
- **ワイルドカード**: ワイルド、ワイルドドロー4 (8枚)

### 🎮 ゲーム機能
- ✅ 2-8人のマルチプレイヤー対応
- ✅ 本格的なUNOルール実装
- ✅ UNOコール機能（忘れるとペナルティ）
- ✅ カードスタッキングルール
- ✅ 方向転換とスキップ効果
- ✅ ワイルドカードの色選択
- ✅ 自動リシャッフル機能

### 💫 ユーザーエクスペリエンス
- 📱 レスポンシブデザイン
- 🎨 美しいグラデーションとアニメーション
- 🔄 リアルタイムゲーム状態更新
- 📢 詳細なゲームメッセージ
- 🎯 直感的なカードプレイ判定

## 🚀 クイックスタート

### インストール不要で即プレイ！

1. **ダウンロード**
   ```bash
   git clone https://github.com/SilentMalachite/UNO-like-card_game.git
   cd UNO-like-card_game
   ```

2. **ゲーム開始**
   - `uno_card_game.html` をブラウザで開く
   - または、ローカルサーバーを起動:
   ```bash
   python3 -m http.server 8000
   # http://localhost:8000/uno_card_game.html にアクセス
   ```

3. **プレイ開始**
   - プレイヤー数を選択 (2-8人)
   - プレイヤー名を入力
   - 「ゲーム開始」をクリック

## 🎯 ゲームルール

### 基本ルール
1. 各プレイヤーに7枚のカードを配布
2. 捨て札の一番上のカードと**色**または**数字**が一致するカードをプレイ
3. 手札が1枚になったら**UNO**をコール（忘れると2枚ペナルティ）
4. 最初に手札を全て出したプレイヤーが勝利

### アクションカード
| カード | 効果 |
|--------|------|
| 🚫 **スキップ** | 次のプレイヤーをスキップ |
| 🔄 **リバース** | ゲーム進行方向を逆転 |
| ➕2️⃣ **ドロー2** | 次のプレイヤーが2枚引いてスキップ |
| 🌈 **ワイルド** | 好きな色を指定 |
| 🌈➕4️⃣ **ワイルドドロー4** | 好きな色を指定＋次のプレイヤーが4枚引いてスキップ |

### 特殊ルール
- **カードスタッキング**: ドロー2にドロー2を、ワイルドドロー4にワイルドドロー4を重ねて効果を累積可能
- **UNOコール**: 手札1枚時に自動的にUNOボタンが表示、次のターンまでにコールしないとペナルティ

## 🛠️ 技術仕様

### ファイル構成
```
UNO-like-card_game/
├── uno_card_game.html     # メインゲームファイル
├── test_results.html      # テスト結果ページ
├── README.md              # このファイル
├── LICENSE                # ライセンス
├── CONTRIBUTING.md        # 貢献ガイド
└── docs/                  # 追加ドキュメント
    └── GAME_RULES.md      # 詳細ルール説明
```

### 技術スタック
- **Frontend**: HTML5, CSS3, Vanilla JavaScript
- **スタイル**: CSS Grid, Flexbox, CSS Animations
- **互換性**: モダンブラウザ (Chrome, Firefox, Safari, Edge)

### アーキテクチャ
```javascript
// ゲーム状態管理
gameState = {
    players: [],           // プレイヤー情報
    deck: [],             // 山札
    discardPile: [],      // 捨て札
    currentPlayerIndex: 0, // 現在のプレイヤー
    direction: 1,         // ゲーム進行方向
    pendingDraw: 0,       // 累積ドロー数
    unoCallRequired: {}   // UNOコール管理
}
```

## 🧪 テスト

### 自動テスト実行
```bash
# ブラウザでtest_results.htmlを開く
open test_results.html
```

### テスト項目
- ✅ デッキ作成 (108枚の正確な構成)
- ✅ カードプレイ可能性判定
- ✅ アクションカード効果
- ✅ ワイルドカード機能
- ✅ スタッキングルール
- ✅ UNOコール機能

## 🎨 スクリーンショット

### ゲーム開始画面
プレイヤー数とプレイヤー名を設定してゲームを開始

### ゲームプレイ画面
- プレイヤー情報グリッド表示
- 中央に山札と捨て札
- 下部に現在プレイヤーの手札
- ゲーム進行方向インジケーター

## 🤝 コントリビューション

プロジェクトへの貢献を歓迎します！詳細は [CONTRIBUTING.md](CONTRIBUTING.md) をご覧ください。

### 貢献方法
1. このリポジトリをフォーク
2. 機能ブランチを作成 (`git checkout -b feature/amazing-feature`)
3. 変更をコミット (`git commit -m 'Add amazing feature'`)
4. ブランチにプッシュ (`git push origin feature/amazing-feature`)
5. プルリクエストを作成

## 📝 ライセンス

このプロジェクトは MIT License の下で公開されています。詳細は [LICENSE](LICENSE) ファイルをご覧ください。

## 🐛 バグレポート・機能要望

バグを発見した場合や新機能の要望がある場合は、[Issues](https://github.com/SilentMalachite/UNO-like-card_game/issues) でお知らせください。

### バグレポートに含めてほしい情報
- 使用ブラウザとバージョン
- 再現手順
- 期待される動作
- 実際の動作
- スクリーンショット（可能であれば）

## 🏆 今後の予定

- [ ] オンラインマルチプレイヤー機能
- [ ] AIプレイヤー追加
- [ ] カスタムルール設定
- [ ] ゲーム統計・スコア記録
- [ ] モバイルアプリ版
- [ ] 音響効果とBGM

## 👥 作者

**あなたの名前** - [@SilentMalachite](https://github.com/SilentMalachite/)

プロジェクトリンク: [https://github.com/SilentMalachite/UNO-like-card_game](https://github.com/SilentMalachite/UNO-like-card_game)

## 🙏 謝辞

- UNOのオリジナルゲームデザインに敬意を表します
- テストとフィードバックを提供してくれた全ての貢献者に感謝

---

⭐ このプロジェクトが気に入ったら、ぜひスターをつけてください！
