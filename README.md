# 批次照片裁切 / 更名工具

純前端、單一檔案的網頁工具。可批次匯入照片、用相機現拍、邊緣裁切（像素或比率）、依試算表欄位批次更名，最後打包成一個 ZIP 下載。**所有處理都在瀏覽器本機完成，照片不會上傳到任何伺服器。**

## 功能

- **批次匯入**：一次選 50＋ 張，或直接把照片拖進視窗，依匯入順序排列並編號。
- **相機拍照**：開相機連拍一組，縮圖勾選要使用的，再加入主清單一起處理（手機可切換前／後鏡頭）。
- **批次裁切（邊緣）**：設定上、下、左、右各裁多少，單位可選像素 `px` 或比率 `%`，按「套用到全部」。每張卡片即時預覽裁切結果與輸出尺寸。
- **個別裁切**：每張卡片可單獨調整裁切量，不受批次覆蓋。
- **批次更名**：從試算表複製一整欄貼上（一行一個檔名），依照片順序對應；可用卡片上的 ◀ ▶ 微調順序。
- **輸出**：維持原格式或轉 JPEG／PNG／WebP、可調品質，全部打包成單一 `photos_日期.zip`。

## 線上使用（GitHub Pages，建議）

透過 GitHub Pages 以 HTTPS 開啟，**相機在 Chrome／Edge／Safari 都能正常使用**。

1. 建立一個新的 GitHub repository。
2. 把 `index.html`、`template-overlay.png`（拍照參考框，需與 index.html 放在同一層）以及這份 `README.md` 上傳到 repo。
3. 進入 repo 的 **Settings → Pages**。
4. **Source** 選 `Deploy from a branch`，分支選 `main`、資料夾選 `/ (root)`，按 **Save**。
5. 等一兩分鐘，用 `https://你的帳號.github.io/你的repo名/` 開啟即可。

## 本機使用

- 直接雙擊 `index.html` 即可使用裁切、更名、打包等所有功能。
- **唯一例外是相機**：以 `file://` 開啟時，Chrome／Edge 會基於安全性擋掉相機。若需在本機用相機，請改用 Firefox，或在此資料夾啟動本機伺服器：

  ```bash
  python -m http.server
  ```

  然後瀏覽器開 `http://localhost:8000/index.html`。

## iPad 拍照版（`ipad-camera.html`）

把拍照功能獨立出來的版本，適合在 iPad 上拍、再回電腦編輯：全螢幕後鏡頭、人像參考框、連拍選取，按一鍵把這組照片打包成 ZIP 並**直接上傳到你的 Google 雲端**。也保留「下載 ZIP（備援）」。

需要與 `template-overlay.png` 放在同一層，且因為要登入 Google，**必須以 https（GitHub Pages）開啟**，不能用 file:// 雙擊。

### 一鍵上傳前的 Google 設定（只需做一次）

1. 到 [Google Cloud Console](https://console.cloud.google.com/) 建立一個專案。
2. 「API 和服務 → 程式庫」啟用 **Google Drive API**。
3. 「OAuth 同意畫面」選 External，填好應用程式名稱，並把自己的 Google 帳號加進「測試使用者」。
4. 「憑證 → 建立憑證 → OAuth 用戶端 ID」，類型選 **網頁應用程式**。
5. 「已授權的 JavaScript 來源」加入你的網站來源，例如 `https://你的帳號.github.io`（只填來源、不含路徑）。
6. 複製 Client ID，開啟 `ipad-camera.html` → 右上「設定」貼上、按儲存。

之後流程：拍照 → 勾選 → 按「打包並上傳 Google Drive」→ 第一次會跳出 Google 授權，同意後就會把 `photos_日期.zip` 上傳到雲端指定資料夾（預設「iPad拍照上傳」，可在設定改）。回電腦從雲端下載解壓，再用 `index.html` 做批次裁切與更名。

上傳使用 `drive.file` 權限，只能存取本工具自己建立的檔案，不會讀取你雲端的其他資料。

## 隱私

裁切／更名工具（`index.html`）不含任何分析、追蹤或上傳行為，照片只存在於你目前的瀏覽器分頁中，關閉分頁即清除。拍照版（`ipad-camera.html`）僅在你按下「上傳」時，把打包檔送到你自己的 Google 雲端。

## 授權

可自由使用與修改。
