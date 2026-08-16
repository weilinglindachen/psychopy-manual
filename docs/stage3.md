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

確認 Builder 上方為 `Run`，填入 `participant = test01`、`session = 001`，完整跑一次 4 trials，逐一確認以下功能仍正常：

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

示意如下：

| A `trial_id` | B `item_id` | D `sentence_type` | E `correctAns` |
|---|---|---|---|
| S01-C | S01 | C | j |
| S01-V | S01 | V | f |
| S02-C | S02 | C | j |
| S02-V | S02 | V | f |

依此規則建立 `S01-C`／`S01-V` 到 `S24-C`／`S24-V`，共 48 trials。

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

| A `trial_id` | D `sentence_type` | F `music_type` | G `music_pair` | H `audio_file` |
|---|---|---|---|---|
| S01-C | C | I | M01 | `audio/M01-I.wav` |
| S01-V | V | R | M01 | `audio/M01-R.wav` |
| S02-C | C | R | M01 | `audio/M01-R.wav` |
| S02-V | V | I | M01 | `audio/M01-I.wav` |

依此規則將 S03–S24 對應到 M02–M12（每個 music pair 對應兩個 item，共 4 個 trials）。

!!! info "注意"
    - `P01` 是 practice，不放入正式 48 trials
    - 每個 music pair 會出現 4 個 trials
    - 每個正式音檔會在 48 trials 中使用 2 次

### 9. 完整檢查 48-trial 條件表

完成後請逐項確認：

- [x] 共有 48 trials
- [x] S01–S24 每個 item 都有 C/V 兩版
- [x] `correctAns`：C = j；V = f
- [x] 每個句子都有 5 words
- [x] `sentence` 與 `word1`–`word5` 一致
- [x] `music_type` 只有 R/I
- [x] `music_pair` 只有 M01–M12
- [x] `audio_file` 與 `music_type`、`music_pair` 一致
- [x] 所有 `audio_file` 都以 `audio/` 開頭
- [x] 所有正式音檔都是 `.wav`
- [x] 沒有空白欄位
- [x] 沒有漏題或重複 trial

---

## 任務 10：檢查四種條件是否平衡

用任何方式確認（例如手動數、或用 Excel 公式），48 個 trials 的四種條件應該平均分布：

| Condition | Count |
|---|---:|
| C + R | 12 |
| C + I | 12 |
| V + R | 12 |
| V + I | 12 |

每種條件內，subject 為 singular／plural 的句子也應該各占一半：

| Condition | Singular | Plural | Total |
|---|---:|---:|---:|
| C + R | 6 | 6 | 12 |
| C + I | 6 | 6 | 12 |
| V + R | 6 | 6 | 12 |
| V + I | 6 | 6 | 12 |

整體 C/V 與 R/I 也應各占一半：

| Sentence type | Count |
|---|---:|
| C | 24 |
| V | 24 |

| Music type | Count |
|---|---:|
| R | 24 |
| I | 24 |

### 任務 10 完成標準

- [x] C + R = 12（6 singular + 6 plural）
- [x] C + I = 12（6 singular + 6 plural）
- [x] V + R = 12（6 singular + 6 plural）
- [x] V + I = 12（6 singular + 6 plural）
- [x] C = 24
- [x] V = 24
- [x] R = 24
- [x] I = 24

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

### 1. 建立 PsychoPy 最終正式檔並讀取檔案

依照上述限制排好固定順序，建立 `conditions_final.xlsx`，並在 `trials` Loop 中把 Conditions 改成這個檔案。成功載入後應看到：

```text
48 conditions, with 13 parameters
```

### 2. 設定 Loop 並先跑前 4 trials 測試

在 `trials` Loop 中確認：

| 欄位 | 設定 |
|---|---|
| Loop type | `sequential` |
| Num. repeats | `1` |
| Selected rows | `0,1,2,3` |
| Random seed | 空白 |
| Conditions | `conditions_final.xlsx` |

因為 pseudorandom order 已經排好，所以不要再使用 random。

Run 時可填 `participant = test02`、`session = 001`。

跑完後請確認前四題順序與音檔：

```text
S02-V → M01-I.wav
S15-C → M08-I.wav
S18-V → M09-R.wav
S19-C → M10-I.wav
```

同時檢查：

- [x] 500 ms fixation 正常
- [x] 五個 words 正常呈現
- [x] 正式音檔有播放
- [x] word/chord 同步正常
- [x] 第五個 word 有句點
- [x] 第五個 onset 後可以按 `f`/`j`
- [x] RT、accuracy 正常
- [x] 音樂不會被截斷
- [x] 沒有 error

### 3. 恢復完整 48 trials

4-trial 測試成功後，再次打開 `trials` Loop，把 `Selected rows = 0,1,2,3` 刪除、恢復空白，確認設定與步驟 2 相同，按 OK 並儲存 `.psyexp`。

### 4. 完整跑一次 48 trials

Run（`participant = test03`、`session = 001`），確認：

- [x] 48 trials 全部跑完
- [x] 所有正式音檔都能找到
- [x] 所有句子正常顯示
- [x] word/chord 同步正常
- [x] fixation timing 正常
- [x] 第五個 onset 後才開始反應
- [x] `f`/`j` 正常記錄
- [x] 音樂不會被截斷
- [x] 沒有 error
- [x] 實驗可以正常結束

### 5. 檢查輸出的 CSV

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

- [x] CSV 有 48 個正式 trials
- [x] 沒有漏 trial
- [x] 沒有重複 trial
- [x] PsychoPy timing 欄位有正常寫入

---

## 第三階段完成檢查表

- [x] 任務 9：建立完整 48-trial 條件表
- [x] 任務 10：檢查四種條件是否平衡
- [x] 任務 11：設定固定 pseudorandom trial order，並完成 48-trial 正式測試與 CSV 驗證

➡️ 接下來進入第四階段：完成受試者實際看到的實驗。
