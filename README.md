# 7B 羽球社 v3 開發專案

這是由目前部署版重建的可編輯 Vite 專案。

## 開發

```bash
npm install
npm run dev
```

## 建置部署版

```bash
npm run build
```

部署 Netlify 時可直接上傳 `dist`，或設定：

- Build command: `npm run build`
- Publish directory: `dist`

## 本版的重要修正

- 保留現有球員、計分、發球員、候場、統計、備份及即時同步功能。
- 同步模式（備份頁可切換，本機記住選項）：
  - **比賽中只同步比分（預設）**：加分時只上傳 `match`；球局結束再同步戰績／候場。
  - **整包同步（舊規則退路）**：維持原本每次操作都上傳完整房間資料。
- 每場結束會優先寫入戰績，並永久寫入：
  `badmintonRooms/{roomId}/matchHistory/{matchId}`。
- 戰績上傳失敗會暫存本機並自動重試；下一場可先本機開打，不需等待重資料傳完。
- 寫入失敗時會顯示同步異常，不再完全靜默。

部署前請將 `FIRESTORE_RULES.txt` 的規則更新到 Firebase Console。
