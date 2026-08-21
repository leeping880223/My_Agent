# 2026 自動化展參觀分享：對話介面（chatbox）與語音操作｜2026-08-28 例會

分享人：李秉則｜參觀日期：2026-08-19、08-20｜地點：南港展覽館

> **投影片版**：[internship-share-2026-08-28.pptx](internship-share-2026-08-28.pptx)（2 頁，簡報體，每頁留一塊區域自行插入影片；另附 PDF）。本檔是完整版底稿，投影片只取兩家的公司介紹與現場重點。

**這次挑兩家專講「怎麼用一句話指揮機器人」**：FANUC 與 Solomon 所羅門。兩家攤位都掛了 NVIDIA 的合作標示（FANUC 是「NVIDIA 2026 Partner」，Solomon 則是「SOLOMON | NVIDIA」並列）。

---

## 一、FANUC｜生成 AI × 機器人：語音操作（Voice Your Command）

**攤位配置**：CRX-10iA 協作手臂＋iRVision 相機、一支立架麥克風、一塊 Scrabble 拼字板與字母托盤、一台平板（示教器）、一面標題牆「**生成 AI×機器人　語音操作！／Generative AI × Robot, Voice Your Command!**」，以及「FANUC Physical AI 概念展示」立牌。

### chatbox 介面拆解（現場螢幕）

畫面分三欄：

| 欄位 | 內容 |
|---|---|
| **左：系統狀態** | SYSTEM CONNECTION（IP `192.168.0.1`、Status **Online**、FTP Server **Online**、Robot State **NORMAL**）／SYSTEM CONTROL（Home Pos、Reset、Start Demo、Stop Demo、Clean Tray）／**LANGUAGE：中文・English・日本語** |
| **中：程式碼** | `ROBOT_CONTROLLER.PY`——可看到 `from robot_interface import robot_interface`、`from robot.scrabble_controller import scrabble_controller`、`target_word = "DRAGON"`、`move = scrabble_engine.find_specific_word_move(board_state, available_letters, target_word)` |
| **右：對話框（MESSAGES）** | 輸入框寫著 "Type an instruction here."，下方 **SEND／CLEAR** 兩顆按鈕 |

### 實際互動（我在現場看到的兩次）

**日文那次**——輸入「ドラゴンをかけてください（請寫 DRAGON）」，系統逐則回覆：

1. 「まずボードとトレイの状態を確認します…」（先確認棋盤與托盤狀態）
2. 「DRAGON を書きます…」（開始寫 DRAGON）
3. 「書き終わりました！」（寫完了）
4. 「単語の書き込みが完了しました！」（單字寫入完成）

**中文那次**——指令是「拼出兩個日本大學的英文縮寫」，系統回「正在為您拼出 KU…」「正在為您拼出 NIT…」，最後「I have finished spelling the words for you!」

### 三個值得抄的設計

1. **語音與文字並存**：主打的是語音（現場架了麥克風、標語就叫 Voice Your Command），但介面同時保留文字輸入框與 SEND 鍵。展場很吵，語音辨識不見得可靠——**留一條文字路徑是務實的做法**，我們自己做 demo 時也該這樣設計。
2. **逐步回報進度，而不是做完才說話**：從「先確認狀態」到「開始寫」到「完成」，使用者隨時知道機器人在做什麼。這對非工程背景的操作者特別重要。
3. **LLM 產生的是「呼叫既有 API 的高階指令」，不是關節角度**：從程式碼看得出來，模型輸出的是 `pick_letter()`、`find_specific_word_move()` 這一層。**換句話說，要做這種 demo 不必等端到端的大模型，用現有的控制與視覺就能先接出可用版本。**

另外，語言可以在中文／English／日本語之間切換，同一套系統直接換介面語言。

---

## 二、Solomon 所羅門（攤位 M400）｜一句話讓人形機器人去把東西拿回來

**現場配置**：一台雙足人形機器人（頭部有球形多感測器罩、雙手為五指靈巧手），面對一個布置成藥局／診間的場景（視力表、藥罐、飲料瓶、木質檯面）；牆上一面大螢幕顯示對話介面。同區另有 UR 手臂裝在 MiR 移動平台上的複合機器人，搭配英業達機櫃展示資料中心應用。

### 實際互動（現場錄影）

操作者輸入的中文指令是完整的一串複合任務：

> 「所以呢，找到葡萄汁，走過去拿起來，並且走回起始位置拿給我。」

系統的回覆是：

> 「找到了。**clear grape juice bottle** 大約在正前方 5 公尺。」

接著人形機器人就自己執行——**找到 → 走過去 → 拿起 → 走回 → 交給人**。

另一面螢幕跑的是他們的 **AOA（Automatic Object Analytics）**：即時的人體骨架偵測與物件偵測畫面，狀態列有 Watching／Detector／Streaming／**Inference time**。

### 兩個關鍵觀察

1. **回覆裡把「它以為自己看到什麼」講出來**——不是只回「好的，執行中」，而是明確說出辨識到的物件名稱（clear grape juice bottle）與大概距離。這等於**把視覺辨識的結果攤開給使用者確認**：如果它認錯了，人在機器人動作之前就能發現。這一點我認為比對話介面本身更值得學。
2. **一句話涵蓋多個步驟**：指令包含移動、抓取、返回、交付四個動作，不是單步命令。系統要自己把一句話拆成任務序列。

**輸入方式**：Solomon 這套是**文字輸入**（螢幕上的 AI Chat 打字下指令），與 FANUC 主打語音的做法不同。兩家並列剛好呈現兩種選擇：**語音重展示效果，文字重可靠度**。

---

## 對我們的三點意義

1. **對話介面已經是這類展示的標準做法**，而且兩家的底層邏輯一致：**語言負責理解與規劃，實際動作交給既有的視覺與控制**。這條路不必等新模型才能開始。
2. **輸入方式：語音與文字各有取捨**——FANUC 主打語音但保留文字框，Solomon 直接用文字。展場吵雜、醫療現場戴口罩，**文字（或選單式）在可靠度上有實際優勢**；建議我們做成雙軌，語音當亮點、文字當保險。
3. **回報設計比指令解析更影響體感**：逐步回報進度（FANUC）、把辨識結果講出來讓人確認（Solomon）——這兩個細節，是讓非工程人員敢用的關鍵。
