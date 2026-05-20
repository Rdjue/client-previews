# 客戶提案上傳交接說明

集中式上傳流程:每個案子在各自的「規劃對話」討論與產出,完成後丟進收件匣 `_inbox/`;由單一的「上傳對話」統一驗證、整理、commit + push。好處是標準一致、git 不會亂、只有上傳對話需要 gh 授權。

```
規劃對話 A ─┐
規劃對話 B ─┼─→  _inbox/<代號>/  ─→  上傳對話(這個 repo 的維運對話)  ─→  GitHub Pages
規劃對話 C ─┘     (HTML + meta.yml)      驗證 / notes / README / commit / push
```

---

## A. 給「規劃對話」的指示

提案定案後,規劃對話只需做 4 件事(**不要碰 git**):

1. 在 `D:\Dropbox\telluswork\client-previews\_inbox\<代號>\` 建資料夾(代號:英文小寫 3–10 字,不含空格/底線/中文)。
2. 把所有 HTML 存進去;**必須有一個 `index.html`** 當落地頁,並用相對連結指向其他 HTML(例 `<a href="wireframe.html">`)。
3. 同資料夾放一個 `meta.yml`,格式見 `_inbox/_TEMPLATE/meta.yml`。
4. 完成後告訴使用者代號即可。

### 可直接貼給規劃對話的一行指示

```
提案定案後,請把所有 HTML 存到 D:\Dropbox\telluswork\client-previews\_inbox\<代號>\,
並在同資料夾放一個 meta.yml(格式見該路徑下 _TEMPLATE\meta.yml)。
務必有一個 index.html 當落地頁、用相對連結指向其他 HTML。
技術規範見 client-previews\HANDOFF.md 的「C. 技術規範」。不要碰 git,完成後告訴我代號。
```

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

## C. 技術規範(每個 HTML 都須符合)

- 單一檔案自含:所有 CSS / JS inline 在該 HTML 裡(不依賴 sibling .css / .js)。
- 不可使用 `localStorage` / `sessionStorage`(跨主機會壞)。
- 外部資源只能引用公開 CDN:Google Fonts、jsDelivr、cdnjs。
- 不可使用需要 build 的格式(JSX 原始碼、TypeScript、SCSS 等);要用 React/Vue 請走 CDN production build。
- 必須 RWD,桌機 / 平板 / 手機皆正常。
- 中文字型用 Noto Sans TC / Noto Serif TC 或同等繁中字型。
- 圖片佔位用公開 placeholder(例 https://placehold.co/),不要把 base64 大圖塞進檔案。
- 編碼存成 UTF-8(無 BOM),檔尾不要有多餘 null byte。

---

## meta.yml 範例

```yaml
代號: muan
類型: 更新            # 新案 / 更新
客戶名稱: 沐恩動物醫院  # 新案必填;更新可省略
聯絡人: 林文傑          # 新案必填;更新可省略
email: jakelinvet@gmail.com
版本: v1.2
日期: 2026-05-21
狀態: 進行中            # 新案用;更新可省略
變更摘要:
  - 修正首頁 banner 文案
檔案說明:
  index.html: 提案說明與導覽(落地頁)
  wireframe.html: 可點擊的互動式 Wireframe 原型
```
