# テトリス 仕様書

## 概要

React + Vite + Tailwind CSS で構築する、PCブラウザ向けテトリスゲーム。

---

## ゲーム詳細

### フィールド

| 項目 | 値 |
|------|-----|
| 横 | 10タイル |
| 縦 | 20タイル |

### テトロミノ

7種類（I, O, T, S, Z, J, L）

| 名前 | 形状 | 色 |
|------|------|-----|
| I | 一直線 | シアン `#06b6d4` |
| O | 2x2四角 | 黄色 `#eab308` |
| T | T字 | 紫 `#a855f7` |
| S | ずらしS | 緑 `#22c55e` |
| Z | ずらしZ | 赤 `#ef4444` |
| J | J字 | 青 `#3b82f6` |
| L | L字 | 橙色 `#f97316` |

### 操作

| キー | 動作 |
|------|------|
| ← → | 左右移動 |
| ↓ | ソフトドロップ |
| ↑ / Z | 時計回り回転 |
| X | 反時計回り回転 |
| Space | ハードドロップ |
| Shift | Hold（保持） |
| P | ポーズ |
| Enter | スタート / リトライ |

### スコア

| アクション | ポイント |
|-----------|---------|
| 1ライン消去 | 100 |
| 2ライン消去 | 300 |
| 3ライン消去 | 500 |
| 4ライン消去（テトリス） | 800 |
| ソフトドロップ | 1pt/タイル |
| ハードドロップ | 2pt/タイル |

### ゲームステート

```
[待機] → (Enter/Space) → [プレイ]
[プレイ] → (P) → [ポーズ]
[プレイ] → (ゲームオーバー) → [ゲームオーバー]
[ゲームオーバー] → (Enter) → [待機]
```

### 保存（localStorage）

```json
{
  "highScore": 0,
  "totalGames": 0,
  "totalLines": 0,
  "lastPlayed": "2025-01-01T00:00:00.000Z"
}
```

ゲーム終了時にスコア更新があれば上書き。

---

## 実装される機能

- [x] 10×20 のフィールド
- [x] 7種類のテトロミノ（7-bag randomizer）
- [x] CW 回転（簡易ウォールキック）
- [x] Ghost Piece（落下位置ガイド）
- [x] Hold（Shift、再保持不可）
- [x] Next Piece（プレビュー）
- [x] ソフトドロップ（↓押し続け）
- [x] ハードドロップ（Space）
- [x] ランディング（30tick = 1.5秒硬直）
- [x] スコア（1〜4ライン消去、ドロップ加点）
- [x] レベル制（速度上昇）
- [x] ゲームオーバー（上部固定）
- [x] 保存（localStorage: ハイスコア・累計）
- [x] ゲームステート（idle / playing / paused / gameover）
- [x] ダークモード、ネオン調、アニメーション
- [x] PCキーボード操作のみ

---

## 実装されない機能

- T-Spin / テコ判定
- Combo / Multi Combo
- 4行同時消去のライン消去
- 回転によるライン消去
- ソフト/ハードドロップ中のライン消去
- モバイル対応（タッチ操作）
- 音效（BGM/SE）
- オンラインランキング
- 難易度モード（ミニット等）

---

## 技術スタック

| 項目 | 技術 |
|------|------|
| フレームワーク | React 19+ |
| ビルドツール | Vite 6+ |
| スタイル | Tailwind CSS 4+ |
| 言語 | TypeScript |
| 保存 | localStorage |
| テスト | Playwright |

---

## ファイル構成（予定）

```
src/
├── main.tsx
├── App.tsx
├── components/
│   ├── Field.tsx
│   ├── Piece.tsx
│   ├── HoldPiece.tsx
│   ├── NextPiece.tsx
│   ├── Stats.tsx
│   └── Controls.tsx
├── hooks/
│   ├── useGameLoop.ts
│   ├── useGameState.ts
│   └── useStorage.ts
├── lib/
│   ├── tetromino.ts
│   ├── field.ts
│   └── scoring.ts
├── types/
│   └── game.ts
└── styles/
    └── globals.css
```
