# 藏書金字塔 · Maslow Library Pyramid

一個以馬斯洛五層需求為架構的 3D 藏書閣。從外部點擊金字塔任一層 → 進入該層大廳（第一人稱、可走動、可轉視角）。左牆是分類書櫃＋平板目錄，右牆是「我的心得」（可讀／改／新增，存於瀏覽器 localStorage）。

## 檔案結構

```
index.html               主程式（GitHub Pages 根網址會自動載入）
support.js               執行階段（必須與 index.html 同目錄，請勿改動）
uploads/
  palace_export.json      藏書檔案（書名 + 樓層），可自行編輯
README.md
```

## 本機執行

因為大廳會用 `fetch()` 讀取 `uploads/palace_export.json`，**不能用 `file://` 直接雙擊開啟**（瀏覽器會擋跨來源讀取）。請用一個本機伺服器：

```bash
# 在專案資料夾下
python3 -m http.server 8000
# 然後瀏覽器開 http://localhost:8000/
```

## 部署到 GitHub Pages

1. 把整個資料夾推上 repo。
2. Settings → Pages → 由 `main` 分支根目錄發佈。
3. 造訪 `https://<帳號>.github.io/<repo>/` —— `index.html` 會自動載入。

## 藏書資料格式

`uploads/palace_export.json`：

```json
{
  "files": ["書名一.md", "書名二.md", "..."],
  "floors": { "書名一.md": 1, "書名二.md": 5 }
}
```

- `floors` 的數字是該書所屬的馬斯洛層級（1–5）。
- 系統會依書名關鍵字自動分到該層底下的分類書櫃。
- 若要精準分類，可在每本書另外指定分類（需要時告訴我，我幫你把程式改成直接讀 `category` 欄位）。

## 心得資料

心得存在瀏覽器 `localStorage`（key：`pyramid_notes_v1`），可在編輯視窗單篇「匯出 JSON」。
