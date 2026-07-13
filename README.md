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
- 啟用 Firestore 網頁離線持久化快取。
- 每場結束除更新房間的 `history` 陣列外，也會永久寫入：
  `badmintonRooms/{roomId}/matchHistory/{matchId}`。
- 寫入失敗時會顯示同步異常，不再完全靜默。

部署前請將 `FIRESTORE_RULES.txt` 的規則更新到 Firebase Console。
