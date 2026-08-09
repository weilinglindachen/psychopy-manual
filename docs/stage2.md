# 第二階段：加入音樂與正式時間安排

**任務 5–8**

第二階段將第一階段的句子判斷核心擴充成：

```text
500 ms fixation
→ 3600 ms 五個 chord／word 刺激
→ 由第五個 word/chord onset 開始記錄反應
→ 最長 3000 ms 反應時間窗
```

完成後會得到一個包含音樂、句子、按鍵、RT 與正確率的四題迷你版完整實驗。

---

## 任務 5：建立並整理測試音檔

### 目標

先用技術測試音檔確認 PsychoPy 能正確找到、播放並切換音檔；這些檔案不作為正式研究刺激。

### 1. 建立 audio 資料夾

在實驗資料夾內建立：

```text
Jessy_psychopy/
├── practice01.psyexp
├── conditions_test.xlsx
├── audio/
└── data/
```

音檔必須放在 `audio` 資料夾中，不要放進 `data`。

### 2. 準備統一使用的 3600 ms 技術測試音檔

第二階段只需要以下兩個檔案：

```text
audio/test_regular_3600ms.wav
audio/test_irregular_3600ms.wav
```

📁 [下載測試音檔（Google Drive）](https://drive.google.com/drive/folders/1XIwGA9CwXdRRfIka0FCBMA9FCj9shvGS?usp=drive_link)

每個 `.wav` 都包含完整的五個 chords，總長 3600 ms：

```text
600 + 600 + 600 + 600 + 1200 ms
```

這兩個檔案會一路用於任務 6、任務 7 與任務 8：

- 任務 6：先固定播放 Regular 音檔，測試 Sound component
- 任務 7：由 Excel 在 Regular 與 Irregular 之間切換
- 任務 8：沿用同一組音檔，設定五個 words 與五個 chords 的 timing

先在 Finder 中各自播放 3600 ms 版本，確認：

- 兩個檔案都能開啟
- 兩者的結尾和弦確實不同
- 每個檔案都包含五個 chords
- 檔名與副檔名完全正確

??? bug "遇到問題：PsychoPy 找不到音檔"
    檢查相對路徑是否從 `.psyexp` 所在位置開始。正確寫法為：

    ```text
    audio/test_regular_3600ms.wav
    ```

    不要只寫 `test_regular_3600ms.wav`，也不要填 Finder 顯示的完整電腦路徑。

---

## 任務 6：加入 Sound component

### 目標

先讓四個 trials 都播放同一個固定音檔，確認 Sound component 本身正常。

### 1. 在 trial Routine 加入 Sound

點右側 Components 中的 **Sound**，設定：

| 欄位 | 設定 |
|---|---|
| Name | `music` |
| Start | `0.0`（初次技術測試） |
| Stop / Duration | 留白 |
| Sound | `audio/test_regular_3600ms.wav` |

Playback 分頁：

| 選項 | 設定 |
|---|---|
| Volume | `1` |
| Hamming window | 勾選 |
| Stop with Routine | 勾選 |
| Force end of Routine | 不勾選 |

### 2. 執行固定音檔測試

確認 Builder 上方為 `Run`（不是 `Pilot`），再點 Desktop 區域的綠色播放鍵。跳出 Participant 視窗時填入 `participant`、`session`（`session` 記得遞增），執行四題，確認每一題都能播放相同音檔。先讓音檔完整播完，再按 `f` 或 `j`。

!!! info "提醒：視窗標題可能仍顯示原始名稱"
    即使 Sound properties 視窗標題仍出現類似 `sound_1 Properties`，只要 Name 欄已設成 `music`，通常不影響執行。以 Builder Routine 中顯示的 component 名稱為準。

---

## 任務 7：讓 Excel 控制不同音檔

### 目標

讓每個 trial 依照 Excel 的 `audio_file` 欄位播放指定音檔。

### 1. 在條件表新增 audio_file

在 `conditions_test.xlsx` 新增 `audio_file` 欄位：

| trial_id | audio_file |
|---|---|
| S01-C | `audio/test_regular_3600ms.wav` |
| S01-V | `audio/test_irregular_3600ms.wav` |
| S02-C | `audio/test_irregular_3600ms.wav` |
| S02-V | `audio/test_regular_3600ms.wav` |

儲存並關閉 Excel。

### 2. 重新載入 Loop 條件表

回到 PsychoPy Builder，在 Flow 中雙擊灰色的 `trials`，重新選取 `conditions_test.xlsx`。確認顯示 `audio_file`：

```text
4 conditions, with 5 parameters
[trial_id, sentence, sentence_type, correctAns, audio_file]
```

??? bug "遇到問題：已修改 Excel，但 Loop 看不到新欄位"
    PsychoPy 可能仍使用先前讀入的欄位資訊。可以先試試看點 Conditions 欄位右側的**綠色箭頭**重新讀取一次；沒有用的話，再重新選取一次 conditions file，或先清除再重新指定。

### 3. 修改 Sound component

在 `trial` Routine 中雙擊 `music`。

在 **Basic** 分頁，把 Sound 從固定路徑：

```text
audio/test_regular_3600ms.wav
```

改成：

```text
$audio_file
```

並確認右側的 Update 是 `set every repeat`。

### 4. 驗證播放順序

確認 Builder 上方為 `Run`，再點 Desktop 的綠色播放鍵執行（Participant 視窗記得填 `participant`、遞增的 `session`）。四題應依序播放：

```text
regular
irregular
irregular
regular
```

---

## 任務 8：設定正式 trial timing

### 目標

建立五個 word 與五個 chord 的同步呈現。每個 trial 的刺激部分為 3600 ms，前方另有 500 ms fixation。

### 1. 正式時間設計

| Trial time | Relative to music onset | Screen / Sound | Duration |
|---:|---:|---|---:|
| 0.0–0.5 s | — | fixation `+` | 500 ms |
| 0.5–1.1 s | 0.0–0.6 s | word1 + chord 1 | 600 ms |
| 1.1–1.7 s | 0.6–1.2 s | word2 + chord 2 | 600 ms |
| 1.7–2.3 s | 1.2–1.8 s | word3 + chord 3 | 600 ms |
| 2.3–2.9 s | 1.8–2.4 s | word4 + chord 4 | 600 ms |
| 2.9–4.1 s | 2.4–3.6 s | word5 + chord 5 | 1200 ms |
| 2.9–5.9 s | — | Keyboard response window | 3000 ms |

重要區分：

```text
五個 chord／word = 3600 ms
fixation = 額外 500 ms
刺激結束時間 = trial 的 4.1 秒
最晚反應時間 = trial 的 5.9 秒
```

RT 從第五個關鍵 word／chord 出現時開始計算，即 trial 的 `2.9 s`。

### 2. 沿用任務 7 的 3600 ms 技術測試音檔

任務 8 不需要再建立或更換音檔，直接沿用任務 7 已設定的 `test_regular_3600ms.wav` / `test_irregular_3600ms.wav`。

每個檔案包含完整五個 chords，時長依序為 `600 + 600 + 600 + 600 + 1200 ms`。

如果已在任務 7 完成 `audio_file` 設定，這一步只需確認，不必再次修改。

### 3. 讓音樂在 fixation 結束後開始

目前 fixation 是 0.0–0.5 秒。請在 `trial` Routine 中雙擊 `music`。

在 **Basic** 分頁，把：

```text
Start = 0
```

改成：

```text
Start = 0.5
```

`Stop / Duration` 繼續留白，其他設定先不動。

這樣正式時間會是：

```text
0–500 ms：fixation
500–4100 ms：五個 chords，共 3600 ms
```

### 4. 把句子拆成五個欄位

目前 Excel 原本已有 A–E 欄，請從 **F 欄開始**新增五個逐字欄位，完成後應該像這樣：

| Excel 欄位 | A | B | C | D | E | F | G | H | I | J |
|---|---|---|---|---|---|---|---|---|---|---|
| 欄位名稱 | `trial_id` | `sentence` | `sentence_type` | `correctAns` | `audio_file` | `word1` | `word2` | `word3` | `word4` | `word5` |

!!! warning "不要刪除 B 欄原本的 sentence"
    `sentence` 保留完整句子，方便之後核對刺激內容；`word1`–`word5` 則供 PsychoPy 逐字呈現。兩者會同時保留在 Excel 中。

測試內容應填成：

| A | B | F | G | H | I | J |
|---|---|---|---|---|---|---|
| trial_id | sentence | word1 | word2 | word3 | word4 | word5 |
| S01-C | The angry man often punches. | The | angry | man | often | punches. |
| S01-V | The angry man often punch. | The | angry | man | often | punch. |
| S02-C | The angry men often punch. | The | angry | men | often | punch. |
| S02-V | The angry men often punches. | The | angry | men | often | punches. |

儲存、關閉 Excel，再重新選取 Loop 的 conditions file。此時應看到 10 個主要條件欄位：

```text
trial_id, sentence, sentence_type, correctAns, audio_file,
word1, word2, word3, word4, word5
```

### 5. 將原句子 component 改為 word1

在 `trial` Routine 中雙擊原本的 `sentence_text`，在同一個設定視窗中修改，把原本 `sentence_text` 改為：

| 欄位 | 設定 |
|---|---|
| Name | `word1_text` |
| Start | `0.5` |
| Stop type | `duration (s)` |
| Duration | `0.6` |
| Text | `$word1` |
| Update | `set every repeat` |

這代表第一個字會與第一個 chord 同時出現：

```text
500–1100 ms：word1 + chord 1
```

### 6. 新增 word2–word5 Text components

所有 words 使用相同畫面位置與文字格式。從 word2 開始，都要在 `trial` Routine 中**新增一個 Text component**（不是修改既有的）。

**word2**

| 欄位 | 設定 |
|---|---|
| Name | `word2_text` |
| Start | `1.1` |
| Stop type | `duration (s)` |
| Duration | `0.6` |
| Text | `$word2` |
| Update | `set every repeat` |

```text
1.1–1.7 秒：word2 + chord 2
```

**word3**

| 欄位 | 設定 |
|---|---|
| Name | `word3_text` |
| Start | `1.7` |
| Stop type | `duration (s)` |
| Duration | `0.6` |
| Text | `$word3` |
| Update | `set every repeat` |

```text
1.7–2.3 秒：word3 + chord 3
```

**word4**

| 欄位 | 設定 |
|---|---|
| Name | `word4_text` |
| Start | `2.3` |
| Stop type | `duration (s)` |
| Duration | `0.6` |
| Text | `$word4` |
| Update | `set every repeat` |

```text
2.3–2.9 秒：word4 + chord 4
```

**word5**

| 欄位 | 設定 |
|---|---|
| Name | `word5_text` |
| Start | `2.9` |
| Stop type | `duration (s)` |
| Duration | **`1.2`** |
| Text | `$word5` |
| Update | `set every repeat` |

```text
2.9–4.1 秒：word5 + chord 5
```

??? bug "遇到問題：Stop 應填 0.6 還是結束時間？"
    當左側選單是 `duration (s)` 時，右側填的是「持續時間」，不是結束時間。

    例如 word2：

    ```text
    Start = 1.1
    Duration = 0.6
    顯示區間 = 1.1–1.7 s
    ```

檢查點：音樂（`music`，Start `0.5`）與 `word1_text` 都在 0.5 秒同時開始。

### 7. 設定 Keyboard 與 RT 起點

雙擊 `sentence_response`：

**Basic**

| 欄位 | 設定 |
|---|---|
| Start | `2.9` |
| Stop type | `duration (s)` |
| Duration | `3.0` |
| Allowed keys | `'f','j'` |
| Force end of Routine | 不勾選 |

**Data**

| 欄位 | 設定 |
|---|---|
| Store | first key |
| Store correct | 勾選 |
| Correct answer | `$correctAns` |

這樣 RT 從第五個關鍵 word／chord onset 開始。

取消 `Force end of Routine` 的原因是：受試者即使在第五個刺激尚未播放完時按鍵，也不會把音檔和 word5 截斷。Routine 會固定持續到反應時間窗結束。

### 8. 執行 timing 測試

確認 Builder 上方為 `Run`，再點 Desktop 的綠色播放鍵執行（Participant 視窗記得填 `participant`、遞增的 `session`）。每題應依序呈現：

```text
+
The
angry
man／men
often
punch／punches
```

請等到第五個字出現後才按 `f` 或 `j`。完成四題後檢查：

- 每次只出現一個 word
- 五個 words 順序正確
- 第五個字停留得比前四個字久
- 音樂完整播放到結尾
- 按鍵後不會立即截斷刺激或提早進入下一題

### 9. 檢查 CSV

成功測試的 CSV 應包含：

```text
trial_id
audio_file
word1–word5
sentence_response.keys
sentence_response.corr
sentence_response.rt
sentence_response.started
word5_text.started
music.started
music.stopped
participant
session
```

實際測試結果：

- 4 個 trials 都成功寫入
- 按鍵依序為 `j, f, j, f`
- 四題 `corr` 均為 `1`
- RT 約為 1.51–1.88 秒
- `word5_text.started` 與 `sentence_response.started` 同時開始
- 音樂與五個 words 都完整呈現

!!! info "檔名不一定包含 session"
    實際輸出檔名可能是：

    ```text
    pilot_practice01_2026-08-06_20h51.31.142.csv
    ```

    預設檔名包含 participant、實驗名稱與時間戳記，不一定包含 `session`。Session 仍會寫在 CSV 的 `session` 欄中。輸入 `009` 後，CSV 內可能顯示為數值 `9`，這是正常的。

    因此找資料時，以「participant + 最新時間」為主，不要只搜尋 `pilot_009`。

---

## 第二階段完成檢查表

- [x] 任務 5：整理測試音檔
- [x] 任務 6：加入 Sound component
- [x] 任務 7：讓條件表控制不同音檔
- [x] 任務 8：設定正式 trial timing

完成第二階段後，四題迷你實驗已能：

- 顯示 500 ms fixation
- 播放 Excel 指定的五和弦音檔
- 將五個 words 與五個 chords 同步呈現
- 從第五個關鍵 word/chord onset 開始記錄 RT
- 接受 `f/j` 判斷
- 自動記錄正確率
- 保留足夠反應時間而不截斷音樂
- 將刺激條件、按鍵、RT、正確率與 timing 寫入 CSV

➡️ 接下來進入 [第三階段：擴充成完整 48 trials](stage3.md)。
