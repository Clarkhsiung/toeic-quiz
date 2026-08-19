# 多益實戰字彙特訓場 — GitHub Pages 部署說明

## 檔案結構

部署時 `index.html` 與 `toeic_vocabulary.json` 必須放在**同一層資料夾**（例如都放在 repo 根目錄），檔名須完全一致（含大小寫），因為網頁是用相對路徑 `fetch('toeic_vocabulary.json')` 自動讀取資料庫：

```
your-repo/
├── index.html
└── toeic_vocabulary.json
```

## 部署步驟

1. 在 GitHub 建立一個新的 repository（Public 或 Private 皆可，Private 需付費方案才能開啟 Pages）。
2. 將 `index.html` 與 `toeic_vocabulary.json` 上傳到 repo 根目錄並 commit / push。
3. 進入 repo 的 **Settings → Pages**。
4. 在 **Build and deployment → Source** 選擇 `Deploy from a branch`。
5. **Branch** 選擇 `main`（或你的預設分支），資料夾選擇 `/ (root)`，按 **Save**。
6. 等待 1～3 分鐘，頁面上方會出現網址，例如：
   `https://<你的帳號>.github.io/<repo名稱>/`
7. 開啟該網址即可使用；右上角應顯示「☁ toeic_vocabulary.json」代表成功自動讀取資料庫。

## 更新單字庫

之後若要更新題庫，只需要覆蓋（replace）repo 裡的 `toeic_vocabulary.json` 並 push，**不需要修改 `index.html`**。GitHub Pages 有 CDN 快取，更新後若頁面沒有變化，請等待數分鐘或用 `Ctrl+F5`（強制重新整理）。

## 疑難排解

- **右上角顯示「內建範例資料（找不到 toeic_vocabulary.json）」**：代表 fetch 失敗，最常見原因是：
  - `toeic_vocabulary.json` 沒有跟 `index.html` 放在同一層
  - 檔名打錯或大小寫不同
  - JSON 格式錯誤（可先用線上 JSON 驗證工具檢查）
- 也可以直接點右上角「上傳題庫 JSON」手動選擇檔案，不受自動讀取失敗影響。
- 若要在本機測試（非 GitHub Pages），建議用本機伺服器開啟而非直接雙擊檔案，例如：
  ```bash
  python -m http.server 8000
  ```
  再開啟 `http://localhost:8000/index.html`。直接用 `file://` 開啟時瀏覽器會封鎖 fetch，此時會自動退回內建的少量範例資料。

##資料庫來源

Name: Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)
Link: https://creativecommons.org/licenses/by-sa/4.0/
