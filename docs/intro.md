# 開始之前：認識 PsychoPy

### Builder

**Builder** 是 PsychoPy 提供的「不用寫程式」視覺化介面，開啟 PsychoPy 後預設會看到它：

- 整個實驗是用一個個 **Routine**（例如 `trial`）組成
- 每個 Routine 裡再放入不同的 **component**（文字、聲音、鍵盤反應等）
- 畫面下方的 **Flow** 決定 Routine 的執行順序與重複次數（例如加上 Loop 重複讀取 Excel 的每一列）

[![PsychoPy Builder 畫面標示：Routine、Components、Flow 三大區塊](assets/builder_terms.png)](assets/builder_terms.png){: .screenshot-link target="_blank" }

在 Builder 右側的 Components 面板中，你會看到很多圖示，例如：

[![PsychoPy Builder components：Slider、Image、Mouse、Text、Sound、Keyboard](assets/comp.png)](assets/comp.png){: .screenshot-link target="_blank" }

簡單說明每一個的功能：

| Component | 功能 |
|---|---|
| **Slider** | 呈現一條可拖曳的量表（例如 Likert scale），讓受試者用滑鼠評分或評等。 |
| **Image** | 在畫面上顯示圖片檔案（例如 `.png`、`.jpg`）。 |
| **Mouse** | 記錄滑鼠點擊位置、點擊時間，或判斷是否點在特定區域內。 |
| **Text** | 在畫面上顯示文字，例如指導語、fixation `+`、句子或單字。 |
| **Sound** | 播放音檔（例如 `.wav`），可設定音量、開始/結束時間。 |
| **Keyboard** | 接收並記錄受試者的按鍵反應與 reaction time。 |

!!! tip "這份手冊只會用到三個：Text、Sound、Keyboard"
    - **Text**：顯示 fixation 與逐字呈現的句子（第一階段就會用到）
    - **Keyboard**：接收 `f/j` 反應並記錄 RT（第一階段就會用到）
    - **Sound**：播放五和弦音檔（第二階段才會用到）

    Slider、Image、Mouse 目前用不到，先不用理會，之後若實驗設計有變動再另外說明。

### Runner

**Runner** 是 PsychoPy 用來實際執行實驗、顯示執行紀錄的視窗。在 Builder 按下綠色播放鍵後，PsychoPy 會自動切換到 Runner 畫面並開始執行。

[![PsychoPy Runner 視窗，顯示 Desktop/Browser/Pavlovia 執行選項與 Stdout 執行紀錄](assets/runner.png)](assets/runner.png){: .screenshot-link target="_blank" }

- 上方的 **Pilot / Run** 切換開關：決定用哪種模式執行
- **Desktop**：在本機視窗中執行實驗（這份手冊主要使用這個）
- **Browser**／**Pavlovia**：透過瀏覽器或線上平台執行，目前不會用到
- 下方的 **Stdout** 分頁：顯示實驗執行過程的完整記錄，包含警告訊息（例如 dropped frames）以及最後是否出現 `Experiment completed`
