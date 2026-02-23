# 2人対戦オンライン釣りバトル実装

## Implementation Checklist

- [x] PeerJS CDN追加 (`peerjs@1.5.4`)
- [x] メニュー画面 HTML/CSS (`#menu-screen`)
- [x] バトルHUD HTML/CSS (`#battle-hud`)
- [x] リザルト画面 HTML/CSS (`#result-screen`)
- [x] 相手キャッチ通知トースト (`#opponent-toast`)
- [x] バトル用グローバル変数追加
- [x] メニュー画面ロジック (`showMenuScreen`, `startFreePlay`, `startBattle`)
- [x] PeerJS ルーム作成/参加 (`createRoom`, `joinRoom`, `setupConnection`)
- [x] メッセージプロトコル (`handlePeerMessage` - assign/start/catch/status/timer/end/rematch)
- [x] バトルタイマー (`startBattleTimer` - ホスト管理、ゲスト同期)
- [x] リザルト/再戦 (`endBattle`, `showResult`, `requestRematch`, `backToMenu`)
- [x] 招待リンク (`copyInviteLink` - Web Share API / clipboard)
- [x] `showCatchPopup` 修正 (バトル時: battleScore加算、catch送信、自動閉じ)
- [x] `fishEscaped` 修正 (バトル時: ステータス送信、自動閉じ)
- [x] `startCasting` / `triggerBite` / `startFight` 修正 (ステータス送信)
- [x] `openShop` 修正 (バトル中は無効)
- [x] セーブラッパー修正 (バトル中はセーブしない)
- [x] 初期化フロー変更 (メニュー画面から開始)
- [x] `handleAction` ガード追加 (メニュー/リザルト画面中は無効)

## Verification

- [x] HTML構造: タグの整合性確認済み
- [x] JavaScript: Node.js `--check` でシンタックスエラーなし
- [x] 全ID参照: HTML内に全て存在確認済み
- [x] onclick ハンドラー: 全関数定義済み
- [x] バトルフロー: menu → connect → battle → result → rematch/menu 確認済み

## Review

933行の単一HTMLファイルに全実装を収めた。主な設計判断:
- ホストが権限を持つ (タイマー管理、最終判定)
- 釣りはローカル実行、スコア/ステータスのみ同期
- バトル中はショップ/セーブ/リセット無効
- ポップアップは1.5秒で自動閉じ (バトルテンポ維持)
- URL パラメータで招待リンク対応
