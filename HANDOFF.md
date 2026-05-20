# 客戶提案上傳交接說明

集中式上傳流程:每個案子在各自的「規劃對話」討論與產出,完成後丟進收件匣 `_inbox/`;由單一的「上傳對話」統一驗證、整理、commit + push。好處是標準一致、git 不會亂、只有上傳對話需要 gh 授權。

```
規劃對話 A ─┐
規劃對話 B ─┼─→  _inbox/<代號>/  ─→  上傳對話(這個 repo 的維運對話)  ─→  GitHub Pages
規劃對話 C ─┘     (HTML + meta.yml)      驗證 / notes / README / commit / push
```

## 使用者只需記兩句話

| 對象 | 你說的話 |
|------|----------|
| **新的規劃 / 提案對話** | 「現在要進行提案交付,請依 `D:\Dropbox\telluswork\client-previews\DELIVERY.md` 的文件說明進行。」 |
| **上傳對話**(本 repo 的維運對話) | 「**處理 inbox**」(或「處理 inbox 的 `<代號>`」) |

---

## A. 給「規劃對話」的指示

規劃對話該做的事,全部寫在 **[`DELIVERY.md`](DELIVERY.md)**(一份自足文件:交付步驟 + 技術規範 + `meta.yml` 格式)。把新的提案對話指向那份文件即可,不必在這裡重複。

重點摘要:規劃對話完成後,把所有 HTML(含一個 `index.html` 落地頁)+ 一個 `meta.yml` 放進 `_inbox/<代號>/`,**不碰 git**。

---

## B. 給「上傳對話」的指示

使用者說「**處理 inbox**」(或「處理 inbox 的 `<代號>`」)時,執行:

1. 掃描 `_inbox/`,逐一處理每個案子資料夾(略過 `_TEMPLATE`)。
2. 讀該資料夾 `meta.yml`。
3. 對每個 HTML 做技術自檢:
   - 確認有 `index.html`,且 `index.html` 內有相對連結指向其他 HTML。
   - grep 確認無 `localStorage` / `sessionStorage`。
   - 檢查編碼:若檔案含結尾 null byte 或非 UTF-8,修正(剝除 null、轉 UTF-8 無 BOM)。
4. 把檔案搬進正式 `<代號>/`(覆蓋既有檔)。
5. notes:
   - 類型=新案 → 依 `shenhe/notes.md` 格式新建 `<代號>/notes.md`(可讀提案 HTML 補充內容)。
   - 類型=更新 → 在既有 `notes.md` 版本歷程新增一列。
6. 更新根目錄 `README.md` 專案索引表(新案加列;更新改版本+日期)。
7. 一次 `git add` 全部 → commit → push。
8. 刪除該案子在 `_inbox/` 的資料夾(清空收件匣)。
9. 回報每個案子的線上網址 `https://rdjue.github.io/client-previews/<代號>/`。

---

## C. 技術規範與 meta.yml 格式

技術規範(單一自含檔、禁用 localStorage/sessionStorage、只用公開 CDN、RWD、UTF-8 無 BOM 等)與 `meta.yml` 欄位格式,以 **[`DELIVERY.md`](DELIVERY.md)** 為唯一準據,避免兩處重複維護而產生落差。`meta.yml` 範本另見 `_inbox/_TEMPLATE/meta.yml`。

上傳對話在驗證階段,以 `DELIVERY.md` 的「技術規範」為檢查清單。
