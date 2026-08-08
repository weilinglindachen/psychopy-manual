# PsychoPy 音樂 × 語言實驗建置手冊（網站版）

這個 repo 是 PsychoPy 音樂 × 語言實驗建置手冊的網站化版本，使用 [MkDocs Material](https://squidfunk.github.io/mkdocs-material/) 產生，並透過 GitHub Actions 自動部署到 GitHub Pages。

## 網站更新方式

之後要新增/修改內容，**只需要編輯 `docs/` 資料夾裡的 `.md` 檔案，然後 push 到 `main` 分支**，網站會在 1–2 分鐘內自動重新部署，不需要手動 build。

```bash
git add docs/
git commit -m "更新第三階段內容"
git push
```

## 檔案結構

```text
.
├── docs/                  ← 網站內容都在這裡，改這裡的 .md 檔就好
│   ├── index.md           ← 首頁（五階段總覽）
│   ├── stage1.md          ← 第一階段：任務 1–4
│   ├── stage2.md          ← 第二階段：任務 5–8
│   ├── stage3.md          ← 第三階段：任務 9–11（待補）
│   ├── stage4.md          ← 第四階段：任務 12–17（待補）
│   └── stage5.md          ← 第五階段：任務 18–22（待補）
├── mkdocs.yml             ← 網站設定（選單、主題、外掛）
├── requirements.txt       ← 建置網站需要的 Python 套件
└── .github/workflows/deploy.yml   ← 自動部署設定，通常不需要改
```

## 常用寫作語法

除了一般的 Markdown 標題、表格、程式碼區塊之外，這份手冊常用兩種提示卡片：

**一般提示／重要說明**（一直展開）：

```markdown
!!! warning "重要：xxx"
    說明文字...
```

可用的類型：`note`、`info`、`tip`、`warning`、`danger`、`bug`。

**除錯說明**（預設收合，點了才展開，適合「遇到問題：...」這種內容）：

```markdown
??? bug "遇到問題：xxx"
    處理方式...
```

## 本機預覽（選用）

如果想在 push 之前先在自己電腦看網站長怎樣：

```bash
pip install -r requirements.txt
mkdocs serve
```

然後瀏覽器開啟 <http://127.0.0.1:8000>。

## 第一次部署設定

1. 到 GitHub 建立一個新的 **public** repository（例如 `psychopy-manual`）。
2. 把這個資料夾 push 上去（見下方指令）。
3. 到 repo 的 **Settings → Pages**，「Build and deployment」的 Source 選擇 `Deploy from a branch`，Branch 選擇 `gh-pages` / `root`，儲存。
4. 等 GitHub Actions 跑完（可在 repo 的 **Actions** 分頁看進度），網站會出現在：

   ```text
   https://<你的帳號>.github.io/<repo名稱>/
   ```

5. 把 `mkdocs.yml` 最上面註解掉的 `repo_url` / `repo_name` 取消註解並填入正確的帳號與 repo 名稱，讓網站右上角出現連到 GitHub 的連結，然後再 commit、push 一次。
