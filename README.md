# 7B 羽球社 v3 開發專案

這是由目前部署版重建的可編輯 Vite 專案。

Firebase 負責房間／比分／戰績／備份資料；前端只是靜態網站。  
省錢做法：**Firebase 保留，前端改放到 Cloudflare Pages**（不要再用 Netlify 燒流量／點數）。

## 開發

```bash
npm install
npm run dev
```

## 建置

```bash
npm run build
```

產出在 `dist/`。PWA 圖示、`manifest`、`sw.js` 會從 `public/` 一併複製進去。

## 建議部署：Cloudflare Pages（免費）

1. 到 [Cloudflare Pages](https://pages.cloudflare.com/) 用 GitHub 帳號登入。
2. 選擇這個 repo：`wasd75412-ctrl/7B`。
3. 建置設定：
   - **Framework preset**: Vite
   - **Build command**: `npm run build`
   - **Build output directory**: `dist`
4. 部署完成後會得到 `*.pages.dev` 網址。
5. 把球友分享連結改成新網址即可。  
   **房間資料仍在 Firebase，不會因為換宿主而消失。**
6. Netlify 站點可直接刪除或停用，避免再被流量暫停／扣點。

手動上傳也可以：本機 `npm run build` 後，把 `dist` 資料夾上傳到 Cloudflare Pages「Direct Upload」。

## 本版的重要修正

- 保留現有球員、計分、發球員、候場、統計、備份及即時同步功能。
- 同步模式（備份頁可切換，本機記住選項）：
  - **比賽中只同步比分（預設）**：加分時只上傳 `match`；球局結束再同步戰績／候場。
  - **整包同步（舊規則退路）**：維持原本每次操作都上傳完整房間資料。
- 房間文件只保留最近 40 場；完整逐場紀錄存於
  `badmintonRooms/{roomId}/matchHistory/{matchId}`。
- 今日／本月／生涯總戰績改讀「房間最近場次 + 雲端完整紀錄」，裁切後不會歸零。
- 戰績上傳失敗會暫存本機並自動重試；下一場可先本機開打，不需等待重資料傳完。
- 寫入失敗時會顯示同步異常，不再完全靜默。
- 建置產物補齊 `sw.js`／PWA 圖示，方便搬到 Cloudflare Pages。

部署前請將 `FIRESTORE_RULES.txt` 的規則更新到 Firebase Console。
