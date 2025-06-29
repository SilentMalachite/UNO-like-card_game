# Contributing to UNO-like Card Game

まず最初に、このプロジェクトへの貢献をご検討いただき、ありがとうございます！🎉

このドキュメントでは、プロジェクトへの貢献方法について説明します。以下のガイドラインに従って、質の高い貢献をお願いします。

## 🤝 貢献の種類

以下のような貢献を歓迎します：

### 🐛 バグ修正
- ゲームロジックの不具合
- UI/UXの問題
- ブラウザ互換性の問題
- パフォーマンスの改善

### ✨ 新機能
- 新しいゲームモード
- UI/UXの改善
- アクセシビリティ機能
- 国際化（i18n）サポート

### 📚 ドキュメント
- README の改善
- コメントの追加・改善
- ゲームルールの詳細化
- チュートリアルの作成

### 🧪 テスト
- 新しいテストケースの追加
- テストカバレッジの向上
- エッジケースのテスト

## 🚀 始め方

### 1. 開発環境のセットアップ

```bash
# リポジトリをフォーク
git clone https://github.com/your-username/UNO-like-card_game.git
cd UNO-like-card_game

# 開発用ブランチを作成
git checkout -b feature/your-feature-name
```

### 2. 開発ツール

このプロジェクトはバニラJavaScriptで構築されているため、特別なビルドツールは必要ありません：

- **推奨エディタ**: VS Code, WebStorm, またはお好みのエディタ
- **推奨ブラウザ**: Chrome DevTools を推奨
- **ローカルサーバー**: `python3 -m http.server 8000` または Live Server拡張

### 3. コードスタイル

#### JavaScript
```javascript
// 良い例
function createDeck() {
    const deck = [];
    
    colors.forEach(color => {
        // 処理...
    });
    
    return deck;
}

// 関数名: camelCase
// 定数: UPPER_SNAKE_CASE
// 変数: camelCase
// インデント: 4スペース
```

#### CSS
```css
/* 良い例 */
.card {
    width: 80px;
    height: 120px;
    border-radius: 10px;
    /* プロパティはアルファベット順 */
}

/* クラス名: kebab-case */
/* インデント: 4スペース */
```

#### HTML
```html
<!-- 良い例 -->
<div class="game-controls">
    <button class="btn btn-primary" onclick="startGame()">
        ゲーム開始
    </button>
</div>

<!-- インデント: 4スペース -->
<!-- 属性値は常にダブルクォート -->
```

## 📋 プルリクエストプロセス

### 1. Issue の確認
- 既存のIssueを確認して、重複していないかチェック
- 大きな変更の場合は、まずIssueで議論することを推奨

### 2. ブランチ命名規則
```bash
# 機能追加
feature/add-ai-player
feature/improve-mobile-ui

# バグ修正
fix/card-stacking-bug
fix/uno-call-penalty

# ドキュメント
docs/update-readme
docs/add-api-docs
```

### 3. コミットメッセージ

コミットメッセージは以下の形式に従ってください：

```
type(scope): 簡潔な説明

詳細な説明（必要に応じて）

Fixes #123
```

**Type:**
- `feat`: 新機能
- `fix`: バグ修正
- `docs`: ドキュメント変更
- `style`: コードフォーマット（機能に影響しない）
- `refactor`: リファクタリング
- `test`: テスト追加・修正
- `chore`: ビルドプロセスやツールの変更

**例:**
```bash
feat(game): add AI player functionality

- Implement basic AI decision making
- Add difficulty level selection
- Update UI to show AI players

Fixes #45
```

### 4. プルリクエストチェックリスト

プルリクエストを作成する前に、以下を確認してください：

- [ ] コードがプロジェクトのスタイルガイドに従っている
- [ ] 新機能にはコメントが適切に追加されている
- [ ] ブラウザで動作テストを実施済み
- [ ] 既存の機能に影響がないことを確認
- [ ] 適切なコミットメッセージを使用
- [ ] README やドキュメントを必要に応じて更新

## 🧪 テストガイドライン

### 手動テスト

新機能や修正後は、以下のテストを実施してください：

1. **基本ゲームフロー**
   - ゲーム開始から終了まで
   - 各アクションカードの動作
   - ワイルドカードの動作

2. **エッジケース**
   - 山札切れ時のリシャッフル
   - UNOコール忘れのペナルティ
   - カードスタッキング

3. **ブラウザ互換性**
   - Chrome, Firefox, Safari, Edge での動作確認
   - レスポンシブデザインの確認

### 自動テスト

```bash
# test_results.html でテスト実行
open test_results.html
```

## 📝 Issue ガイドライン

### バグレポート

バグを報告する際は、以下の情報を含めてください：

```markdown
## バグの概要
簡潔な説明

## 再現手順
1. ゲームを開始
2. プレイヤー数を4人に設定
3. ...

## 期待される動作
何が起こるべきか

## 実際の動作
実際に何が起こったか

## 環境
- OS: macOS 14.0
- ブラウザ: Chrome 120.0
- 画面サイズ: 1920x1080

## 追加情報
- スクリーンショット
- エラーメッセージ
```

### 機能要望

```markdown
## 機能の概要
新機能の簡潔な説明

## 動機
なぜこの機能が必要か

## 詳細な説明
機能の詳細な仕様

## 代替案
他に考えられる解決策
```

## 🎯 優先度の高い貢献エリア

現在、以下のエリアでの貢献を特に歓迎しています：

1. **モバイル対応の改善** - タッチデバイスでの操作性向上
2. **アクセシビリティ** - キーボード操作、スクリーンリーダー対応
3. **国際化** - 多言語サポート
4. **AIプレイヤー** - コンピューター対戦相手の実装
5. **オンラインマルチプレイヤー** - リアルタイム対戦機能

## 💬 コミュニケーション

- **質問**: Issuesで気軽に質問してください
- **議論**: 大きな変更の前にDiscussionsで話し合いましょう
- **レビュー**: プルリクエストでは建設的なフィードバックを心がけます

## 🏆 貢献者への感謝

貢献してくださった全ての方をREADMEの「謝辞」セクションでクレジットします。

## 📖 追加リソース

- [JavaScript Style Guide](https://github.com/airbnb/javascript)
- [HTML5 Best Practices](https://github.com/hail2u/html-best-practices)
- [CSS Guidelines](https://cssguidelin.es/)

---

ご質問がありましたら、お気軽にIssueを作成してください。貢献をお待ちしています！ 🚀