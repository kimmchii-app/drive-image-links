# 雲端圖床連結轉換

把 Google Drive 的分享連結轉成可以直接放進網頁或 Markdown 的圖片網址。

整個工具只有一個 `index.html`，用瀏覽器開啟就能用，不用安裝，也不用登入 Google 帳號。

## 功能

- 一行一個連結，一次可以貼很多行。
- 輸出格式有三種：HTML `<img>`、Markdown `![]()`、純網址。
- 同一行裡連結以外的文字會變成圖片說明（alt）。
- 圖片可以輸出原始尺寸，或指定寬度（px）。
- 網址形式預設用 `lh3.googleusercontent.com`，也可以切換成 `drive.google.com/thumbnail`。
- 每個連結都會實際載入一張縮圖，標示「可顯示」或「無法載入」，忘記開共用的檔案當場看得出來。
- 整行貼上舊的 `<img>` 或 `![]()` 也能轉，原本的說明文字會沿用。
- 資料夾連結、Google 文件、非 Drive 的連結會標出行號和原因。
- 格式、尺寸、網址形式的選擇存在瀏覽器本機，下次開啟沿用。

## 使用方式

1. 在 Google Drive 對圖片按右鍵，選「共用」，把「一般存取權」改成「知道連結的任何人」。
2. 按「複製連結」，貼到輸入框。
3. 選輸出格式，按「複製全部」，或按單張圖片旁的「複製」。

## 範例

輸入：

```
角色立繪 https://drive.google.com/file/d/檔案ID/view?usp=sharing
```

HTML 輸出：

```html
<img src="https://lh3.googleusercontent.com/d/檔案ID=s0" alt="角色立繪" referrerpolicy="no-referrer">
```

Markdown 輸出：

```markdown
![角色立繪](https://lh3.googleusercontent.com/d/檔案ID=s0)
```

HTML 輸出帶的 `referrerpolicy="no-referrer"` 是預防 Google 依來源網站擋圖，不需要可以自行刪掉。

## 支援的連結寫法

- `https://drive.google.com/file/d/檔案ID/view`
- `https://drive.google.com/open?id=檔案ID`
- `https://drive.google.com/uc?export=view&id=檔案ID`
- `https://drive.google.com/thumbnail?id=檔案ID`
- `https://lh3.googleusercontent.com/d/檔案ID`
- 單獨一行的檔案 ID

## 輸出的網址

| 網址形式 | 原始尺寸 | 指定寬度 800 |
| :-- | :-- | :-- |
| lh3.googleusercontent.com | `https://lh3.googleusercontent.com/d/檔案ID=s0` | `https://lh3.googleusercontent.com/d/檔案ID=w800` |
| drive.google.com/thumbnail | `https://drive.google.com/thumbnail?id=檔案ID&sz=s0` | `https://drive.google.com/thumbnail?id=檔案ID&sz=w800` |

指定的寬度超過原圖時，拿到的是原圖大小，不會放大。

## 限制

- 檔案要設成「知道連結的任何人」可以檢視，否則別人看到的是破圖。
- Google Drive 沒有提供正式的圖床服務，這些網址借用的是 Drive 的圖片預覽功能。短時間內讀取次數太多時，Google 會暫時擋掉。個人網站、設定集這類用量通常夠用，流量大的網站請改用正式的圖床。
- 舊的 `https://drive.google.com/uc?export=view&id=檔案ID` 已經不能直接顯示圖片（2026 年 10 月實測），工具不會輸出這種格式。
