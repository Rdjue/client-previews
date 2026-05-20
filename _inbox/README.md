# 收件匣 _inbox/

這是「上傳前的暫存區」。**每個客戶案子的規劃對話**把產出放這裡,負責上傳的對話會來掃描、驗證、搬進正式位置並 push。

## 規劃對話要做的事(只有這些)

1. 在 `_inbox/` 底下建一個以**案子代號**命名的資料夾(英文小寫,例 `muan`)。
2. 把所有 HTML 檔放進去。**必須有一個 `index.html`** 作為落地頁,且它要用相對連結指向其他 HTML(例 `<a href="wireframe.html">`)。
3. 在同資料夾放一個 `meta.yml`,格式見 [`_TEMPLATE/meta.yml`](_TEMPLATE/meta.yml)。
4. **不要碰 git**(不 add / 不 commit / 不 push)。完成後告訴使用者代號即可。

規劃對話的完整指示(交付步驟 + 技術規範 + `meta.yml` 格式)見 repo 根目錄的 [`../DELIVERY.md`](../DELIVERY.md)。整體流程概覽見 [`../HANDOFF.md`](../HANDOFF.md)。

完成後的結構範例:

```
_inbox/
  muan/
    index.html
    wireframe.html
    meta.yml
```

## 上傳對話要做的事

使用者只要說「**處理 inbox**」(或「處理 inbox 的 muan」),上傳對話會:

1. 掃描 `_inbox/` 內每個案子資料夾(略過 `_TEMPLATE`)。
2. 讀 `meta.yml`,並對每個 HTML 做技術自檢(有 `index.html`、無 localStorage/sessionStorage、剝除結尾 null byte、編碼確認)。
3. 把檔案搬進正式 `<代號>/`,新案產生 `notes.md`、更新案子則 bump 版本歷程。
4. 更新根目錄 `README.md` 索引表。
5. 一次 commit + push。
6. 清空該案子在 `_inbox/` 的資料夾。
7. 回報每個案子的線上網址。

## 注意

- `_inbox/` 內的**案子資料夾不會進 git**(由 `.gitignore` 排除),只有本 `README.md` 與 `_TEMPLATE/` 會被追蹤。所以暫存檔不會污染 repo 歷史。
- 因為走 Dropbox 同步,規劃對話與上傳對話只要在同一台機器(或同步到同一個 Dropbox)就能共用這個收件匣。
