# 🔧 UNO風カードゲーム - API仕様

このドキュメントでは、ゲームの内部APIと主要な関数について説明します。開発者がコードを理解し、機能を拡張する際の参考資料として活用してください。

## 📋 目次

1. [ゲーム状態管理](#ゲーム状態管理)
2. [コア関数](#コア関数)
3. [カード関連関数](#カード関連関数)
4. [UI関数](#ui関数)
5. [ユーティリティ関数](#ユーティリティ関数)
6. [イベントハンドラー](#イベントハンドラー)

## 🎮 ゲーム状態管理

### GameState オブジェクト

```javascript
let gameState = {
    players: [],              // プレイヤー配列
    deck: [],                // 山札
    discardPile: [],         // 捨て札
    currentPlayerIndex: 0,    // 現在のプレイヤーインデックス
    direction: 1,            // ゲーム進行方向 (1: 時計回り, -1: 反時計回り)
    gameOver: false,         // ゲーム終了フラグ
    canDraw: true,           // カード引取可能フラグ
    hasDrawn: false,         // カード引取済みフラグ
    unoCallRequired: {},     // UNOコール必要フラグ (プレイヤーインデックス: boolean)
    pendingDraw: 0,          // 累積ドロー数
    canStack: false          // スタッキング可能フラグ
}
```

### Player オブジェクト

```javascript
{
    name: string,    // プレイヤー名
    hand: []         // 手札 (Card配列)
}
```

### Card オブジェクト

```javascript
// 数字カード
{
    type: 'number',
    color: 'red'|'blue'|'green'|'yellow',
    number: 0-9
}

// アクションカード
{
    type: 'action',
    color: 'red'|'blue'|'green'|'yellow',
    action: 'skip'|'reverse'|'draw2'
}

// ワイルドカード
{
    type: 'wild',
    action: 'wild'|'wild-draw4',
    chosenColor?: 'red'|'blue'|'green'|'yellow'  // 選択された色
}
```

## ⚙️ コア関数

### createDeck()

デッキを作成する関数

```javascript
/**
 * 標準UNOデッキ(108枚)を作成
 * @returns {Array<Card>} シャッフル済みデッキ
 */
function createDeck()
```

**動作**:
1. 数字カード76枚を作成
2. アクションカード24枚を作成
3. ワイルドカード8枚を作成
4. シャッフルして返す

### shuffleDeck(deck)

デッキをシャッフルする関数

```javascript
/**
 * Fisher-Yatesアルゴリズムでデッキをシャッフル
 * @param {Array<Card>} deck - シャッフル対象のデッキ
 * @returns {Array<Card>} シャッフル済みデッキ
 */
function shuffleDeck(deck)
```

### canPlayCard(card)

カードがプレイ可能かチェックする関数

```javascript
/**
 * 指定されたカードがプレイ可能かチェック
 * @param {Card} card - チェック対象のカード
 * @returns {boolean} プレイ可能な場合true
 */
function canPlayCard(card)
```

**判定ロジック**:
1. 捨て札が空の場合: true
2. スタッキング中の場合: 同種のドローカードのみ
3. ワイルドカード: 常にtrue
4. 色一致: true
5. 数字一致: true (数字カード同士)
6. アクション一致: true (アクションカード同士)

### playCard(cardIndex)

カードをプレイする関数

```javascript
/**
 * 指定されたインデックスのカードをプレイ
 * @param {number} cardIndex - 手札内のカードインデックス
 */
function playCard(cardIndex)
```

**処理フロー**:
1. プレイ可能性チェック
2. 手札から捨て札への移動
3. 勝利条件チェック
4. UNOコール判定
5. カード効果実行
6. ターン進行

## 🎴 カード関連関数

### executeActionCard(card)

アクションカードの効果を実行

```javascript
/**
 * アクションカードの効果を実行
 * @param {Card} card - 実行するアクションカード
 */
function executeActionCard(card)
```

**処理対象**:
- `skip`: 次プレイヤーをスキップ
- `reverse`: 進行方向を反転
- `draw2`: 次プレイヤーに2枚ドロー + スキップ

### executeWildCard(card)

ワイルドカードの効果を実行

```javascript
/**
 * ワイルドカードの効果を実行
 * @param {Card} card - 実行するワイルドカード
 */
function executeWildCard(card)
```

**処理フロー**:
1. 色選択プロンプト表示
2. 選択色を捨て札に設定
3. ワイルドドロー4の場合: 追加でドロー効果

### renderCard(card, clickHandler, isClickable)

カード要素を作成

```javascript
/**
 * カードのDOM要素を作成
 * @param {Card} card - 描画するカード
 * @param {Function} clickHandler - クリック時のハンドラー
 * @param {boolean} isClickable - クリック可能フラグ
 * @returns {HTMLElement} カードのDOM要素
 */
function renderCard(card, clickHandler = null, isClickable = true)
```

## 🖥️ UI関数

### renderCurrentHand()

現在プレイヤーの手札を表示

```javascript
/**
 * 現在のプレイヤーの手札をUIに表示
 */
function renderCurrentHand()
```

**処理内容**:
1. 手札コンテナをクリア
2. 各カードのDOM要素を作成
3. プレイ可能性に応じてスタイル適用
4. クリックハンドラーを設定

### renderPlayersGrid()

全プレイヤーの情報を表示

```javascript
/**
 * 全プレイヤーの情報グリッドを表示
 */
function renderPlayersGrid()
```

### renderDiscardPile()

捨て札を表示

```javascript
/**
 * 捨て札の一番上のカードを表示
 */
function renderDiscardPile()
```

### updateDisplay()

画面全体を更新

```javascript
/**
 * ゲーム画面全体を更新
 */
function updateDisplay()
```

**更新対象**:
- 現在プレイヤーの手札
- プレイヤー情報グリッド
- 捨て札表示
- 山札カウント
- ターン表示
- ボタン状態

## 🎯 ゲームフロー関数

### startGame()

ゲームを開始

```javascript
/**
 * 新しいゲームを開始
 */
function startGame()
```

**初期化処理**:
1. プレイヤー情報収集
2. ゲーム状態リセット
3. デッキ作成
4. 手札配布 (各7枚)
5. 最初の捨て札設定
6. UI切り替え

### nextPlayer()

次のプレイヤーにターンを移行

```javascript
/**
 * 次のプレイヤーにターンを移行
 */
function nextPlayer()
```

**処理フロー**:
1. UNOコール忘れペナルティチェック
2. プレイヤーインデックス更新
3. スタッキング処理
4. UI更新

### endGame(winnerName)

ゲームを終了

```javascript
/**
 * ゲームを終了し勝者を表示
 * @param {string} winnerName - 勝者名
 */
function endGame(winnerName)
```

## 🃏 ユーティリティ関数

### drawCard()

山札からカードを引く

```javascript
/**
 * 現在のプレイヤーが山札からカードを1枚引く
 */
function drawCard()
```

### reshuffleDeck()

捨て札をシャッフルして山札に戻す

```javascript
/**
 * 捨て札をシャッフルして新しい山札を作成
 * @returns {boolean} 成功した場合true
 */
function reshuffleDeck()
```

### callUno()

UNOをコール

```javascript
/**
 * 現在のプレイヤーがUNOをコール
 */
function callUno()
```

### showMessage(text, duration)

メッセージを表示

```javascript
/**
 * 一定時間メッセージを表示
 * @param {string} text - 表示メッセージ
 * @param {number} duration - 表示時間（ミリ秒）
 */
function showMessage(text, duration = 3000)
```

## 🎨 セットアップ関数

### initSetup()

セットアップ画面を初期化

```javascript
/**
 * ゲーム設定画面を初期化
 */
function initSetup()
```

### updatePlayerNameInputs()

プレイヤー名入力欄を更新

```javascript
/**
 * 選択されたプレイヤー数に応じて入力欄を生成
 */
function updatePlayerNameInputs()
```

## 🔧 カスタマイズポイント

### 新しいカードタイプの追加

1. **カードオブジェクトの拡張**:
   ```javascript
   {
       type: 'special',
       action: 'new-action',
       // 追加プロパティ
   }
   ```

2. **createDeck()の修正**: 新カードを追加
3. **canPlayCard()の修正**: 新ルール追加
4. **executeActionCard()の修正**: 新効果実装
5. **renderCard()の修正**: 新表示対応

### 新しいゲームモードの追加

1. **ゲーム状態の拡張**: 必要なプロパティを追加
2. **初期化処理の修正**: モード固有の設定
3. **勝利条件の変更**: 新しい勝利ルール
4. **UI要素の追加**: モード選択UI

### AI プレイヤーの実装

```javascript
// AI判断関数の例
function makeAIDecision(playerIndex) {
    const player = gameState.players[playerIndex];
    const playableCards = player.hand.filter(canPlayCard);
    
    // 戦略的判断ロジック
    // ...
    
    return selectedCardIndex;
}
```

## 📊 デバッグ機能

### コンソールログ

開発時に有用なログ出力:

```javascript
// デッキ情報
console.log('Deck size:', gameState.deck.length);

// プレイヤー情報
console.log('Players:', gameState.players.map(p => ({
    name: p.name,
    handSize: p.hand.length
})));

// ゲーム状態
console.log('Game state:', {
    currentPlayer: gameState.currentPlayerIndex,
    direction: gameState.direction,
    pendingDraw: gameState.pendingDraw
});
```

---

この API 仕様を参考に、ゲームの機能拡張やカスタマイズを行ってください！ 🚀