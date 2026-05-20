# 提案交付說明(給規劃 / 提案對話讀)

> 開新的客戶提案對話時,使用者會說:
> 「現在要進行提案交付,請依 `D:\Dropbox\telluswork\client-previews\DELIVERY.md` 的文件說明進行。」
> 你讀到這份文件後,就照下面做。

你正在協助蓋婭科技(Tellustek)討論並產出一份**客戶網站提案 / 雛形 HTML**。最終上線由一個集中的「上傳管理對話」統一處理。

**你的範圍只有「把成品放進收件匣」。請勿:**
- ❌ 不要執行任何 git 指令(add / commit / push)。
- ❌ 不要修改 `client-previews` repo 內收件匣以外的任何檔案(README、其他案子資料夾等)。
- ✅ 你只需要:讀本檔、把 HTML + `meta.yml` 寫進收件匣資料夾。

> 權限說明:你需要對 `D:\Dropbox\telluswork\client-previews\_inbox\` 的**讀寫權限**,以及讀取本檔的權限。第一次存取時若跳出權限請求,請使用者允許即可。

---

## 交付步驟(提案內容定案後)

1. **決定案子代號**:英文小寫 3–10 字,不含空格、底線、中文(例:沐恩動物醫院 → `muan`)。
   - 若此案先前已上傳過,沿用既有代號。
2. **存 HTML** 到收件匣資料夾(不存在就建立):
   `D:\Dropbox\telluswork\client-previews\_inbox\<代號>\`
   - **必須有一個 `index.html`** 作為落地頁,並用相對連結指向其他 HTML(例 `<a href="wireframe.html">`)。
3. **寫 `meta.yml`** 到同資料夾,格式照抄並填寫(範本在 `D:\Dropbox\telluswork\client-previews\_inbox\_TEMPLATE\meta.yml`):

   ```yaml
   代號: muan
   類型: 新案            # 「新案」或「更新」
   客戶名稱: 沐恩動物醫院  # 新案必填;更新可省略
   聯絡人: 林文傑          # 新案必填;更新可省略
   email: jakelinvet@gmail.com
   版本: v1              # 例 v1 / v2 / v2.1
   日期: 2026-05-20      # YYYY-MM-DD
   狀態: 進行中           # 新案用;更新可省略
   變更摘要:
     - 首版提案
   檔案說明:             # 可選,每個 HTML 一行,會寫進 notes.md
     index.html: 提案說明與導覽(落地頁)
     wireframe.html: 可點擊的互動式 Wireframe 原型
   ```

4. **回報使用者**:「代號是 `<代號>`,檔案已放進 `_inbox`。請到上傳對話說『處理 inbox』。」

完成後的結構範例:

```
_inbox/
  muan/
    index.html
    wireframe.html
    meta.yml
```

---

## 技術規範(每個 HTML 都必須符合)

- **單一檔案自含**:所有 CSS / JS inline 在該 HTML 內(不依賴外部 .css / .js 檔)。
- **禁用** `localStorage` / `sessionStorage`(跨主機會壞)。
- 外部資源**只能引用公開 CDN**:Google Fonts、jsDelivr、cdnjs。
- 不可使用需要 build 的格式(JSX 原始碼、TypeScript、SCSS);要用 React/Vue 請走 CDN production build。
- 必須 **RWD**,桌機 / 平板 / 手機皆正常呈現。
- 中文字型用 **Noto Sans TC / Noto Serif TC** 或同等繁中字型(Google Fonts)。
- 圖片佔位用公開 placeholder(例 `https://placehold.co/`),不要把 base64 大圖塞進檔案。
- 存成 **UTF-8(無 BOM)**,檔尾不要有多餘 null byte。

---

## 上傳端會做什麼(供你了解,不需你執行)

使用者在上傳對話說「處理 inbox」後,上傳管理對話會:讀 `meta.yml` → 技術自檢 → 把檔案搬進正式 `<代號>/` → 產生或更新 `notes.md` → 更新 `README.md` 索引 → commit + push → 清空收件匣 → 回報線上網址 `https://rdjue.github.io/client-previews/<代號>/`。
