# Client Previews

蓋婭科技 客戶雛形預覽集中區。每個子資料夾是一個客戶案子,內含獨立的 `index.html`,透過 GitHub Pages 服務供客戶線上瀏覽。

## 線上網址結構

```
https://rdjue.github.io/client-previews/<案子代號>/
```

## 專案索引

| 案子代號 | 客戶 | 聯絡人 | 上線網址 | 最新版本 | 狀態 |
|---------|------|--------|----------|----------|------|
| `shenhe` | 深河出版 | YUE-YING LU<br>ameajisai912@gmail.com | [前往](https://rdjue.github.io/client-previews/shenhe/) | v2.1 / 2026-05-19 | 進行中 |
| `muen` | 沐恩動物醫院 | 林文傑<br>jakelinvet@gmail.com | [前往](https://rdjue.github.io/client-previews/muen/) | v1 / 2026-05-20 | 進行中 |

## 加入新案子

1. 在 repo 根目錄建立新資料夾,名稱為「案子代號」(英文小寫,例如 `acme`)
2. 把該案子的 `index.html` 放進資料夾(檔名必須為 `index.html`)
3. 同時建立 `notes.md` 記錄案子資訊(可參考 `shenhe/notes.md` 格式)
4. 更新本 README 的專案索引表
5. Commit & push,網址即刻生效

## 結案處理

- **短期歸檔**:把資料夾移到 `_archive/<案子代號>/`(網址失效,檔案保留)
- **完全下架**:直接刪除資料夾並 commit

## 命名規範

- 案子代號:**英文小寫**,不含空格與中文(避免 URL encode 變亂碼)
- 檔名:每個案子的入口檔必須是 **`index.html`**,GitHub Pages 才會正確路由
- 圖片/影片等資源:放在 `<案子代號>/assets/` 內

## 此 Repo 的維護者

Tellustek (蓋婭科技) — service@tellustek.com
