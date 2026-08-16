# PsychoPy 音樂 × 語言實驗建置手冊

作者：陳韋伶

這份手冊記錄本研究使用 PsychoPy Builder 建置實驗的完整流程。整體工作分為 **五個階段**，每個階段都會先完成一個可獨立測試的版本，再進入下一階段。

!!! tip "如何使用這份手冊"
    進行每個任務時，依序閱讀：

    1. **操作步驟**
    2. **該步驟旁的除錯說明**（點開黃色/紅色提示卡片）
    3. **完成後的驗證方式**

    不要跳過驗證。畫面能正常執行，不一定代表資料有正確記錄；每個階段都應同時檢查 PsychoPy 畫面與 CSV 輸出。

    每完成一個階段，本手冊都會更新一次，加入新增任務的完整操作流程、實際成功驗證方式、常見錯誤與已遇過的問題。

!!! danger "❗️遇到問題時，怎麼辦？（很重要，請務必讀完）"
    手冊裡已經整理了常見的除錯情境，但一定還是會遇到手冊沒寫到的狀況。**遇到卡關時，請不要卡住不動或直接放棄**，建議：

    1. **善用 AI**（例如 ChatGPT、Claude）：把你遇到的狀況直接描述給 AI，或是**截圖你的 PsychoPy 畫面／錯誤訊息，直接貼給 AI 看**。
    2. **請 AI 一個步驟一個步驟說明**，不要一次要求「幫我全部弄好」。例如可以這樣問：

        === "中文"

            ```text
            我在 PsychoPy Builder 遇到這個錯誤（附截圖），
            請你一步一步告訴我要怎麼排查，
            先不要跳步驟，我做完一步再跟你回報結果。
            ```

        === "English"

            ```text
            I ran into this error in PsychoPy Builder (screenshot attached).
            Please walk me through troubleshooting it one step at a time —
            don't skip ahead. I'll report back the result after each step.
            ```

    3. 做完 AI 建議的每一步，都回報結果給 AI（成功／失敗／出現新的訊息），讓它根據實際情況調整下一步，而不是一次貼一大串步驟自己悶著頭做。

    這樣做的好處是排查過程會留下紀錄，也能訓練自己看懂錯誤訊息，之後遇到類似狀況會更快解決。

## 整體五階段規劃

| 階段 | 任務 | 內容 | 狀態 |
|---|---|---|---|
| 第一階段 | 任務 1–4 | 純句子判斷核心：fixation、句子呈現、`f/j` 反應、RT、Excel 條件表、自動判對錯 | ✅ 已完成 |
| 第二階段 | 任務 5–8 | 加入音樂與正式 timing：五和弦音檔、逐字呈現、Excel 控制音檔切換 | ✅ 已完成 |
| 第三階段 | 任務 9–11 | 擴充成完整 48 trials，並檢查四種條件是否平衡 | 🟡 進行中 |
| 第四階段 | 任務 12–18 | 完成受試者實際看到的完整實驗（說明、練習、休息、結束畫面） | 🟡 進行中 |
| 第五階段 | 任務 18–22 | 測試、檢查 CSV、pilot test、正式定稿 | ⬜ 未開始 |

點選左側或上方選單進入各階段的詳細操作步驟。

### 第一階段：完成純句子判斷核心

預計完成：

- fixation
- 句子呈現
- `f/j` 按鍵反應
- reaction time
- Excel 條件表
- 自動讀取不同句子
- 自動判定答對或答錯

完成後會得到一個可獨立運作的「純句子判斷小實驗」。詳見 [第一階段](stage1.md)。

### 第二階段：加入音樂與正式時間安排

預計完成：

- 整理測試音檔
- 加入 Sound component
- 讓 Excel 控制不同音檔
- 設定 fixation、音樂、句子與反應的正式 timing

完成後會得到一個包含音樂、句子、按鍵、RT 與正確率的四題迷你版完整實驗。詳見 [第二階段](stage2.md)。

### 第三階段：擴充成完整 48 trials

預計完成：

- 建立完整 48-trial 條件表
- 檢查四種條件是否平衡
- 設定 trial 呈現順序

四種主要條件為：

| 音樂條件 | 句子條件 |
|---|---|
| Regular | Correct |
| Regular | Violation |
| Irregular | Correct |
| Irregular | Violation |

完成後會得到條件平衡的正式刺激版本。

### 第四階段：完成受試者實際看到的實驗

預計完成：

- practice trials
- 實驗說明畫面
- Practice → Formal experiment 轉場
- 中途休息
- participant 資料欄位
- 結束畫面
- 完整 end-to-end 測試

完成後，實驗即可交由受試者實際操作。詳見 [第四階段](stage4.md)。

### 第五階段：測試、檢查與正式定稿

預計完成：

- 完整跑完 48 trials
- 檢查 CSV
- 建立正式版與備份
- 學生 pilot test
- 根據 pilot 結果修正

完成後會得到可正式收案的最終版本。

## 時程規劃

**2026/08/09**：完成第一、第二階段

1. 顯示 fixation `+`
2. 顯示英文句子（逐字呈現）
3. 接受 `f` 或 `j` 按鍵
4. 記錄反應鍵與 reaction time
5. 從 Excel 依序讀取不同句子與音檔
6. 比較受試者按鍵與正確答案
7. 播放 Excel 指定的五和弦音檔，並與五個 words 同步
8. 在 CSV 中記錄每題答對或答錯、RT 與 timing

## 建議的資料夾結構

```text
Jessy_psychopy/
├── practice01.psyexp
├── conditions_test.xlsx
├── audio/
│   ├── test_regular_3600ms.wav
│   └── test_irregular_3600ms.wav
└── data/
```

!!! warning "注意"
    - `practice01.psyexp` 和 `conditions_test.xlsx` 必須放在同一層。
    - `data` 資料夾會在實驗執行後自動建立。
    - 不要把條件表或音檔放進 `data` 資料夾。
