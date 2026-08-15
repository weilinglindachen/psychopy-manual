# 第三階段：擴充成完整 48 trials

**任務 9–11**

第三階段將 4-trial 迷你實驗擴充成正式的 48-trial 完整實驗：

```text
建立完整 48-trial 條件表
→ 檢查四種條件（C+R、C+I、V+R、V+I）是否平衡
→ 設定固定的 pseudorandom trial 呈現順序
```

完成後會得到條件平衡、順序固定的正式 48-trial 版本。

---

## 任務 9：建立完整 48-trial 條件表

### 1. 建立正式條件檔

把原本成功運作的 `conditions_test.xlsx` 複製一份，重新命名為 `conditions_formal.xlsx`。

!!! warning "保留 conditions_test.xlsx"
    請保留 `conditions_test.xlsx`，不要直接覆蓋，之後仍可能需要回頭比對測試版本。

### 2. 設定正式欄位

正式條件表使用 A–M 共 13 欄，比第二階段多了 `item_id`、`music_type`、`music_pair` 三個新欄位：

| A | B | C | D | E | F | G | H | I | J | K | L | M |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `trial_id` | `item_id` | `sentence` | `sentence_type` | `correctAns` | `music_type` | `music_pair` | `audio_file` | `word1` | `word2` | `word3` | `word4` | `word5` |

### 3. 先用原本 4 trials 測試新欄位

新欄位可先只填測試資料，確認格式沒問題：

| `trial_id` | `item_id` | `music_type` | `music_pair` |
|---|---|---|---|
| S01-C | S01 | R | test |
| S01-V | S01 | I | test |
| S02-C | S02 | I | test |
| S02-V | S02 | R | test |

其他欄位先不改。

### 4. 讓 PsychoPy 重新讀取正式條件表

在 Flow 中雙擊灰色的 `trials` Loop，把 Conditions 從 `conditions_test.xlsx` 改成 `conditions_formal.xlsx`。

成功載入後應看到：

```text
4 conditions, with 13 parameters
```

??? bug "遇到問題：已修改 Excel，但 Loop 看不到新欄位"
    PsychoPy 可能仍使用先前讀入的欄位資訊。可以先點 Conditions 欄位右側的**綠色箭頭**重新讀取一次；沒有用的話，再重新選取一次 conditions file。

### 5. 做 4-trial regression test

確認 Builder 上方為 `Run`，完整跑一次 4 trials，逐一確認以下功能仍正常：

- 500 ms fixation
- 音樂正常播放
- 5 個 words 正常依序出現
- word/chord 同步沒有明顯異常
- 第五個 word/chord onset 後可按 `f`/`j`
- 音樂不會因為按鍵而被截斷
- 4 題都能完整跑完
- 沒有 error

若全部成功，再開始擴充正式 48 trials。

### 6. 建立 48-trial 骨架

正式實驗包含 24 個 base items，每個 item 有 C（Correct）/ V（Violation）兩版，共 48 trials：

| 規則 | 說明 |
|---|---|
| `item_id` | 每個出現兩次（C 與 V） |
| C | `sentence_type = C`，`correctAns = j` |
| V | `sentence_type = V`，`correctAns = f` |

完整 48-trial 骨架如下：

<div class="scrollable-table" markdown>

| A `trial_id` | B `item_id` | D `sentence_type` | E `correctAns` |
|---|---|---|---|
| S01-C | S01 | C | j |
| S01-V | S01 | V | f |
| S02-C | S02 | C | j |
| S02-V | S02 | V | f |
| S03-C | S03 | C | j |
| S03-V | S03 | V | f |
| S04-C | S04 | C | j |
| S04-V | S04 | V | f |
| S05-C | S05 | C | j |
| S05-V | S05 | V | f |
| S06-C | S06 | C | j |
| S06-V | S06 | V | f |
| S07-C | S07 | C | j |
| S07-V | S07 | V | f |
| S08-C | S08 | C | j |
| S08-V | S08 | V | f |
| S09-C | S09 | C | j |
| S09-V | S09 | V | f |
| S10-C | S10 | C | j |
| S10-V | S10 | V | f |
| S11-C | S11 | C | j |
| S11-V | S11 | V | f |
| S12-C | S12 | C | j |
| S12-V | S12 | V | f |
| S13-C | S13 | C | j |
| S13-V | S13 | V | f |
| S14-C | S14 | C | j |
| S14-V | S14 | V | f |
| S15-C | S15 | C | j |
| S15-V | S15 | V | f |
| S16-C | S16 | C | j |
| S16-V | S16 | V | f |
| S17-C | S17 | C | j |
| S17-V | S17 | V | f |
| S18-C | S18 | C | j |
| S18-V | S18 | V | f |
| S19-C | S19 | C | j |
| S19-V | S19 | V | f |
| S20-C | S20 | C | j |
| S20-V | S20 | V | f |
| S21-C | S21 | C | j |
| S21-V | S21 | V | f |
| S22-C | S22 | C | j |
| S22-V | S22 | V | f |
| S23-C | S23 | C | j |
| S23-V | S23 | V | f |
| S24-C | S24 | C | j |
| S24-V | S24 | V | f |

</div>

完成後應有：標題列 + 48 trials = 共 49 列。

### 7. 填入完整句子與五個 words

填入 C `sentence` 與 I–M 欄的 `word1`–`word5`：

| A `trial_id` | C `sentence` | I `word1` | J `word2` | K `word3` | L `word4` | M `word5` |
|---|---|---|---|---|---|---|
| S01-C | The pretty woman often laughs. | The | pretty | woman | often | laughs. |
| S01-V | The pretty woman often laugh. | The | pretty | woman | often | laugh. |

依此完成 S01-C 到 S24-V。

!!! warning "填完句子後務必檢查"
    - 每句都剛好 5 個 words
    - `sentence` 與 `word1`–`word5` 完全一致
    - 第五個 word 是 critical word
    - C/V 只操弄 subject–verb agreement

### 8. 填入正式音樂資訊

正式音樂共有 12 組 music pairs（`M01`–`M12`），每組各有 Regular（R）/ Irregular（I）兩個版本，共 24 個正式 `.wav` 音檔，檔名為 `M01-R.wav`、`M01-I.wav`……`M12-R.wav`、`M12-I.wav`。

依下表填 F `music_type`、G `music_pair`、H `audio_file`：

<div class="scrollable-table" markdown>

| A `trial_id` | D `sentence_type` | F `music_type` | G `music_pair` | H `audio_file` |
|---|---|---|---|---|
| S01-C | C | R | M01 | `audio/M01-R.wav` |
| S01-V | V | I | M01 | `audio/M01-I.wav` |
| S02-C | C | I | M01 | `audio/M01-I.wav` |
| S02-V | V | R | M01 | `audio/M01-R.wav` |
| S03-C | C | R | M02 | `audio/M02-R.wav` |
| S03-V | V | I | M02 | `audio/M02-I.wav` |
| S04-C | C | I | M02 | `audio/M02-I.wav` |
| S04-V | V | R | M02 | `audio/M02-R.wav` |
| S05-C | C | R | M03 | `audio/M03-R.wav` |
| S05-V | V | I | M03 | `audio/M03-I.wav` |
| S06-C | C | I | M03 | `audio/M03-I.wav` |
| S06-V | V | R | M03 | `audio/M03-R.wav` |
| S07-C | C | R | M04 | `audio/M04-R.wav` |
| S07-V | V | I | M04 | `audio/M04-I.wav` |
| S08-C | C | I | M04 | `audio/M04-I.wav` |
| S08-V | V | R | M04 | `audio/M04-R.wav` |
| S09-C | C | R | M05 | `audio/M05-R.wav` |
| S09-V | V | I | M05 | `audio/M05-I.wav` |
| S10-C | C | I | M05 | `audio/M05-I.wav` |
| S10-V | V | R | M05 | `audio/M05-R.wav` |
| S11-C | C | R | M06 | `audio/M06-R.wav` |
| S11-V | V | I | M06 | `audio/M06-I.wav` |
| S12-C | C | I | M06 | `audio/M06-I.wav` |
| S12-V | V | R | M06 | `audio/M06-R.wav` |
| S13-C | C | R | M07 | `audio/M07-R.wav` |
| S13-V | V | I | M07 | `audio/M07-I.wav` |
| S14-C | C | I | M07 | `audio/M07-I.wav` |
| S14-V | V | R | M07 | `audio/M07-R.wav` |
| S15-C | C | R | M08 | `audio/M08-R.wav` |
| S15-V | V | I | M08 | `audio/M08-I.wav` |
| S16-C | C | I | M08 | `audio/M08-I.wav` |
| S16-V | V | R | M08 | `audio/M08-R.wav` |
| S17-C | C | R | M09 | `audio/M09-R.wav` |
| S17-V | V | I | M09 | `audio/M09-I.wav` |
| S18-C | C | I | M09 | `audio/M09-I.wav` |
| S18-V | V | R | M09 | `audio/M09-R.wav` |
| S19-C | C | R | M10 | `audio/M10-R.wav` |
| S19-V | V | I | M10 | `audio/M10-I.wav` |
| S20-C | C | I | M10 | `audio/M10-I.wav` |
| S20-V | V | R | M10 | `audio/M10-R.wav` |
| S21-C | C | R | M11 | `audio/M11-R.wav` |
| S21-V | V | I | M11 | `audio/M11-I.wav` |
| S22-C | C | I | M11 | `audio/M11-I.wav` |
| S22-V | V | R | M11 | `audio/M11-R.wav` |
| S23-C | C | R | M12 | `audio/M12-R.wav` |
| S23-V | V | I | M12 | `audio/M12-I.wav` |
| S24-C | C | I | M12 | `audio/M12-I.wav` |
| S24-V | V | R | M12 | `audio/M12-R.wav` |

</div>

!!! info "注意"
    - `P01` 是 practice，不放入正式 48 trials
    - 每個 music pair 會出現 4 個 trials
    - 每個正式音檔會在 48 trials 中使用 2 次

### 9. 完整檢查 48-trial 條件表

完成後請逐項確認：

- [ ] 共有 48 trials
- [ ] S01–S24 每個 item 都有 C/V 兩版
- [ ] `correctAns`：C = j；V = f
- [ ] 每個句子都有 5 words
- [ ] `sentence` 與 `word1`–`word5` 一致
- [ ] `music_type` 只有 R/I
- [ ] `music_pair` 只有 M01–M12
- [ ] `audio_file` 與 `music_type`、`music_pair` 一致
- [ ] 所有 `audio_file` 都以 `audio/` 開頭
- [ ] 所有正式音檔都是 `.wav`
- [ ] 沒有空白欄位
- [ ] 沒有漏題或重複 trial

---

## 任務 10：檢查四種條件是否平衡

### 1. 新增 Balance_Check 工作表

在 Excel 下方新增一個工作表，命名為 `Balance_Check`，建立：

| A | B |
|---|---|
| Condition | Count |
| C + R | |
| C + I | |
| V + R | |
| V + I | |

假設正式條件表工作表名稱為 `Sheet1`，依序在 B2–B5 輸入：

```excel
=COUNTIFS(Sheet1!D:D,"C",Sheet1!F:F,"R")
=COUNTIFS(Sheet1!D:D,"C",Sheet1!F:F,"I")
=COUNTIFS(Sheet1!D:D,"V",Sheet1!F:F,"R")
=COUNTIFS(Sheet1!D:D,"V",Sheet1!F:F,"I")
```

正確結果應為四種條件各 12：

| Condition | Count |
|---|---:|
| C + R | 12 |
| C + I | 12 |
| V + R | 12 |
| V + I | 12 |

### 2. 檢查整體 C/V 與 R/I

在同一張 `Balance_Check` 工作表加入：

| Sentence type | Count | 公式 |
|---|---:|---|
| C | 24 | `=COUNTIF(Sheet1!D:D,"C")` |
| V | 24 | `=COUNTIF(Sheet1!D:D,"V")` |

| Music type | Count | 公式 |
|---|---:|---|
| R | 24 | `=COUNTIF(Sheet1!F:F,"R")` |
| I | 24 | `=COUNTIF(Sheet1!F:F,"I")` |

### 任務 10 完成標準

- [ ] C + R = 12
- [ ] C + I = 12
- [ ] V + R = 12
- [ ] V + I = 12
- [ ] C = 24
- [ ] V = 24
- [ ] R = 24
- [ ] I = 24

---

## 任務 11：設定 trial 呈現順序

正式實驗不能直接使用 `S01-C → S01-V → S02-C → S02-V ...` 這種順序，因為同一個 base sentence 的兩個版本不能連續出現。

本實驗使用固定的 pseudorandom order，所有受試者使用同一個順序，需符合以下限制：

- 同一個 item 的 C/V 至少間隔 **10 trials**
- 同一個 `music_pair` 至少間隔 **6 trials**
- 同一個實際音檔兩次使用至少間隔 **19 trials**
- C/V 最多連續 **2 題**
- R/I 最多連續 **2 題**

此外，48 個 trials 必須全部出現一次、沒有遺漏、沒有重複，且四種條件（C+R、C+I、V+R、V+I）分散在整個實驗中。

### 1. 建立 Trial_Order 工作表

新增工作表 `Trial_Order`，建立兩欄 `order`、`trial_id`，依序填入排好的 48 筆固定順序：

<div class="scrollable-table" markdown>

| `order` | `trial_id` |
|---:|---|
| 1 | S20-C |
| 2 | S14-V |
| 3 | S12-C |
| 4 | S09-C |
| 5 | S15-V |
| 6 | S04-C |
| 7 | S22-V |
| 8 | S17-C |
| 9 | S07-V |
| 10 | S01-C |
| 11 | S23-V |
| 12 | S06-V |
| 13 | S10-C |
| 14 | S13-V |
| 15 | S15-C |
| 16 | S21-V |
| 17 | S20-V |
| 18 | S18-C |
| 19 | S04-V |
| 20 | S02-C |
| 21 | S07-C |
| 22 | S05-V |
| 23 | S23-C |
| 24 | S12-V |
| 25 | S03-V |
| 26 | S16-C |
| 27 | S21-C |
| 28 | S10-V |
| 29 | S19-V |
| 30 | S24-C |
| 31 | S02-V |
| 32 | S13-C |
| 33 | S08-C |
| 34 | S11-V |
| 35 | S05-C |
| 36 | S18-V |
| 37 | S09-V |
| 38 | S14-C |
| 39 | S16-V |
| 40 | S01-V |
| 41 | S19-C |
| 42 | S06-C |
| 43 | S24-V |
| 44 | S03-C |
| 45 | S22-C |
| 46 | S17-V |
| 47 | S11-C |
| 48 | S08-V |

</div>

### 2. 建立 Final_Conditions 工作表

新增工作表 `Final_Conditions`，第一列使用和正式條件表完全相同的 13 個欄位（A–M）。

假設原始 48-trial 條件表工作表叫 `Sheet1`，`Trial_Order` 的 B 欄是 `trial_id`，在 `Final_Conditions!A2` 輸入：

```excel
=XLOOKUP(Trial_Order!B2,Sheet1!$A$2:$A$49,Sheet1!$A$2:$M$49)
```

按 Enter 後確認 A2–M2 自動帶入完整資料，再把公式往下填到第 49 列。

### 3. 建立 PsychoPy 最終正式檔

另外建立一個新的 Excel 檔案 `conditions_final.xlsx`，把 `Final_Conditions` 的 A1:M49 複製過去。

!!! warning "使用「貼上值」，不要貼公式"
    請使用 **Paste Values / 貼上值**，不要把 `XLOOKUP` 公式一起帶過去。`conditions_final.xlsx` 應只保留乾淨的正式 48-trial 表。

### 4. 讓 PsychoPy 讀取 conditions_final.xlsx

打開 `trials` Loop，把 Conditions 改成 `conditions_final.xlsx`。成功載入後應看到：

```text
48 conditions, with 13 parameters
```

### 5. 設定 Loop

在 `trials` Loop 中確認：

| 欄位 | 設定 |
|---|---|
| Loop type | `sequential` |
| Num. repeats | `1` |
| Selected rows | 空白 |
| Random seed | 空白 |
| Conditions | `conditions_final.xlsx` |

因為 pseudorandom order 已經排好，所以不要再使用 random。

### 6. 先跑前 4 trials 測試

暫時在 `Selected rows` 輸入 `0:4`，其他設定維持 `sequential`、`Num. repeats = 1`、`Random seed` 空白。

Run 時可填 `participant = test02`、`session = 001`。

確認：

- [ ] 音檔正常播放
- [ ] 句子內容正確
- [ ] 500 ms fixation 正常
- [ ] 五個 words/chords 同步
- [ ] 第五個 onset 後可按 `f`/`j`
- [ ] RT 正常
- [ ] accuracy 正常
- [ ] 音樂不被截斷
- [ ] 沒有 error

### 7. 恢復完整 48 trials

4-trial 測試成功後，再次打開 `trials` Loop，把 `Selected rows = 0:4` 刪除、恢復空白，確認設定與步驟 5 相同，按 OK 並儲存 `.psyexp`。

### 8. 完整跑一次 48 trials

Run（`participant = test03`、`session = 001`），確認：

- [ ] 48 trials 全部跑完
- [ ] 所有正式音檔都能找到
- [ ] 所有句子正常顯示
- [ ] word/chord 同步正常
- [ ] fixation timing 正常
- [ ] 第五個 onset 後才開始反應
- [ ] `f`/`j` 正常記錄
- [ ] 音樂不會被截斷
- [ ] 沒有 error
- [ ] 實驗可以正常結束

### 9. 檢查輸出的 CSV

找到剛才完整 48-trial 測試產生的 CSV，確認正式條件欄位都有寫入：

```text
trial_id, item_id, sentence, sentence_type, correctAns,
music_type, music_pair, audio_file, word1–word5
```

並確認 Keyboard component 產生的 `.keys`、`.rt`、`.corr`：

- `.keys` 應記錄 `f` 或 `j`
- `.rt` 應有反應時間
- `.corr`：1 = correct；0 = incorrect

最後確認：

- [ ] CSV 有 48 個正式 trials
- [ ] 沒有漏 trial
- [ ] 沒有重複 trial
- [ ] PsychoPy timing 欄位有正常寫入

---

## 第三階段完成檢查表

- [ ] 任務 9：建立完整 48-trial 條件表
- [ ] 任務 10：檢查四種條件是否平衡
- [ ] 任務 11：設定固定 pseudorandom trial order，並完成 48-trial 正式測試與 CSV 驗證

➡️ 接下來進入第四階段：完成受試者實際看到的實驗。
