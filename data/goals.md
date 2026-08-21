# 長期計畫表

由 goal-planner 建立、plan-adjuster 調整。任務完成後從「即將要做」移到「已完成」。

## 專案：G1 手術器械分揀 + 搬運（碩士論文，與工研院合作）

**目標**：Unitree G1 在 Isaac Sim/Lab 中（1）辨識手術器械並用 Dex3 三爪手實體夾取、分類放置；（2）拿著盒子行走、放到櫃子上。模擬為主，畢業需上實機（工研院採購中）。

**Repo**：https://github.com/leeping880223/Isaac-sim

## 📌 論文題目與方向

> ⚠️ 這一節在 2026-08-20 之前只存在於通訊軟體對話裡，現在補寫進檔案。來源：2026-07-28（週二）與 Prof. Basanta Haobijam 的對話紀錄。

### 為什麼換題目

原本的 RL 題目**不可行**，換到 ITRI 的手術器械專案：

> 「After we collect the data, we found action data is more than perception data, more than 4 times, and perception data is not regular. So that's impossible to do the reinforcement learning.」

教授的回應：既然原本的 RL 專案因臨床資料的限制不再可行，這是合理的替代方向；並認為有 Isaac Sim／Isaac Lab／NVIDIA GR00T 的存取權、又同時有模擬與實機硬體，是做出有意義實驗的重大優勢。

### 教授建議的題目

- 短版：**Autonomous Surgical Instrument Manipulation Using Vision-Language-Action Models in Isaac Lab**
- 長版：**Intelligent Autonomous Surgical Assistant: Integrating Vision-Language-Action Models, Task Planning, and Humanoid Robot Manipulation Using Isaac Sim and Real-Robot Deployment**

### 教授指定的技術主線

現況（教授的描述）：`Image → YOLO → Instrument Detection → 3D Position`
建議延伸為：`Image → YOLO → 3D Pose → Motion Planning → Grasp Planning → Robot Manipulation`

機器人要能**自主**完成：**identify → localize → grasp → hand over → place → organize**

### 教授給的 10 步驟進程（★ 明講「聚焦 4–10」）

| # | 項目 | 狀態 |
|---|---|---|
| 1 | Synthetic data generation | ✅ 已完成 |
| 2 | Instrument segmentation | ✅ 已完成 |
| 3 | 3D localization | ✅ 已完成 |
| 4 | **Pose estimation** | ⬜ |
| 5 | **Motion planning** | ⬜ |
| 6 | **Grasp planning** | ⬜ |
| 7 | **Vision-language understanding** | ⬜ ← chatbox 介面落在這裡（見下方） |
| 8 | **Autonomous manipulation** | ⬜ |
| 9 | **Human-robot collaboration** | ⬜ |
| 10 | **Real-world validation** | ⬜ |

> 教授原話：「You can focus 4–10 sections, if you do, your thesis will be remarkable and applicable to real-time industrial applications.」

### 指導安排 ✅

- **Basanta 教授正式指導**。**楊老師已經簽了**（2026-08-21），行政程序走完，這件事結案。

### 📌 我的盤算（未定案，要拿去跟教授談）

**論文主體＝ITRI 的手術器械 ＋ VLA／chatbox；LEX System 只當履歷專案，不是論文。**

| | 定位 | 期間 |
|---|---|---|
| ITRI 手術器械 ＋ chatbox | **畢業論文主體**，也是研討會論文的來源 | 實習 2026-09 → 12（合約到期）；論文寫作延續到 2027 上半年 |
| LEX System 瑕疵檢測（AOI：缺鍵／錯鍵／空焊） | **履歷專案** | 2027-01 → 06，Basanta 教授主持，每週書面報告＋期中期末 |

**理由**：LEX 2027-01 才開始、06 結束，與 2027 年中口試幾乎同時，撐不起畢業；ITRI 是**現在就能做研究的唯一窗口**，資源在手、主管有 chatbox／VLA 的明確需求，職涯上也對口（達明／台達／Solomon）。兩件事題材不重疊，能帶過去的只有經驗與方法（「用合成資料補缺陷樣本」在 AOI 同樣是痛點）。

**畢業**：2027 年中；門檻為**研討會論文一篇 ＋ 完整研究論文（不必投稿）**。門檻不要求期刊接受，研討會審查快，ITRI 的成果撐得起來。

```
2026-09 ── 12   ITRI：做出 chatbox demo ＋ 實驗數據    ← 唯一的研究窗口
2027-01 ── 03   投研討會論文 ／ LEX 開跑
2027-03 ── 06   學位論文寫作 ＋ LEX 進行 ＋ 口試
```

**要跟教授談的三件事**（談完不行再回來改）：

1. **這個分工他同不同意**——論文主體留 ITRI、LEX 當專案；7/28 定的手術器械 VLA 題目是否維持。
2. **目標研討會與投稿 deadline**——deadline 會倒推 9–12 月的里程碑，他通常有慣用的研討會。
3. **機器人題目他能指導到什麼程度**——影像那一層是他的專長，人形與模擬那層打算找 ITRI 的技術對口補上。

**另外要自己確認**：實習到期後還能不能用 ITRI 的資料與成果寫論文（不能的話整個計畫要重排）。

### ITRI 的分工（進行中）

工研院攤位那台雙臂人形手術器械分揀 demo，**就是使用者實習的那個所展出的**，細節上班就問得到。重點是**分工還在安排中**——要**主動提案**接下 **chatbox／VLA ＋ 影像 grounding** 這一塊，不要等分工分下來。理由現成：實習主管自己說過這塊缺人，它同時是教授 10 步驟的第 7 項、也是論文主線。可帶的籌碼是合成資料 pipeline 已到 mAP50 ~0.9、辨識與 2D→3D 已跑通——**手上有具體進度的人，在分工會議上講話比較有份量。**

### ⚠️ Basanta 教授的專長是影像 → 選題重心

使用者的判斷：**「他是做影像的，最好還是跟影像相關。」**

這條直接決定 10 步驟裡力氣要放哪：

| 步驟 | 與影像的關係 | 建議比重 |
|---|---|---|
| 4 Pose estimation | **純影像**，且是現有 YOLO → 3D position 的直接延伸 | **高** |
| 6 Grasp planning | 抓取姿態多半從影像／點雲算出 | **高** |
| 7 Vision-language understanding | **影像與語言的交集——VLA 的「V」正是教授的地盤** | **高** |
| 5 Motion planning | 幾何與控制為主，影像成分低 | 中 |
| 8 Autonomous manipulation | 整合層 | 中 |
| 9 Human-robot collaboration | 偏系統與任務規劃 | 中（但這是工研院想要的差異化） |
| 10 Real-world validation | 實驗 | 依進度 |

**原則：論文骨幹留在「看得懂 → 算得出姿態 → 抓得起來」這條影像主線；VLA 是把它串起來的介面，不是拿來取代影像。**

### 💬 chatbox 介面

**這一項不是教授指定的，是這次逛展看到、判斷值得加進來的**（詳見 [field-notes](field-notes/2026-08-automation-taipei/README.md)）。

**展場上的三個現成範例**：

| 來源 | 做法 | 可借鑑的地方 |
|---|---|---|
| **FANUC** Physical AI Demo | 右側就是一個 chatbox：打「請寫 DRAGON」→ 回「先確認棋盤與托盤狀態…」→「開始寫…」→「完成！」；程式碼是 LLM 呼叫既有的 `pick_letter()`、`find_specific_word_move()` | **LLM 產生的是「呼叫既有 API 的高階指令」，不是關節角**。而且**逐步回報狀態**，使用者知道機器人在想什麼 |
| **Solomon**（M400） | 打「找到葡萄汁，走過去拿起來，走回起始位置拿給我」→ 回「找到了，clear grape juice bottle 大約在正前方 5 公尺」→ 人形執行 | **回覆裡把「它認為自己看到什麼」講出來**，這是影像 grounding 的可視化 |
| **台達 × NVIDIA** | 架構圖：大腦＝VLM｜LLM｜GPU，小腦＝EtherCAT｜工控 | 分層方式可直接照抄當論文的系統架構圖 |

**★ 需求來源（最關鍵的一條）**：**工研院實習主管明講他們目前較缺 chatbox／VLA 這一塊**——使用者因此才特別注意這個主題。**動機是雙向的**：既是合作單位講出來的缺口，**使用者自己也覺得這件事很酷、想做**（2026-08-21 自述）。需求端與興趣端對齊，是這條線最穩的地方。

**為什麼這一項對本論文特別划算**：

1. **正好落在教授清單第 7 項 vision-language understanding**，不是額外加碼
2. **合作單位（工研院）自己說缺這塊**——需求端已經確認，不必自己說服別人這件事有價值
3. **工研院想推的就是「下指令」**，而且未來要「同一個指令給多台機器人」——chatbox 是那件事的第一步
4. **仍然是影像題**（Basanta 教授的專長）：指令要落到「**哪一支**器械」，靠的是影像 grounding；「把彎鉤剪刀放到綠布上」→ 得先在畫面裡指認出彎鉤剪刀。**語言只是入口，判對判錯還是影像在決定**
5. **demo 效果最好**：口試、實習報告、工研院驗收，打一句話機器人就動，任何人都看得懂

**最小可行做法（不要一開始就上端到端 VLA）**：

```
自然語言指令
  → LLM 解析成結構化的 (動作, 物件, 目標位置)
  → 用現有 YOLO 分割結果在影像中指認該物件（grounding）
  → 呼叫現有的 pick & place / RMPflow
  → 逐步把狀態回報到對話框（看到什麼、要去哪、做完了沒）
```

**對話介面的兩種用途（2026-08-20 由新代科技的做法延伸）**：
1. **指派任務**：下指令 → 執行 → **回報進度**（FANUC、Solomon、台達都是這種）
2. **查詢歷史**：問「資料在哪、這批是誰做的、哪台機器做的」（新代把加工履歷送雲端，再用 Chatbot 查詢）
   - 對照 CSSD：**器械追溯**（這支器械在哪一包、上次哪時候滅菌、誰用過）天生就是第 2 種需求。**主線先做第 1 種，第 2 種可列為延伸或未來工作。**

### 三方期待對照

| 誰 | 想要什麼 | 落差／風險 |
|---|---|---|
| **Basanta 教授** | VLA ＋ 任務規劃 ＋ 自主操作（10 步驟的 4–10）；**清單裡沒有「行走搬運」** | 與 goals.md 現行的階段三（行走、搬盒）對不上 |
| **工研院（ITRI）** | 推 **VLA 應用**：可下指令，**未來同一個指令可以下給多台機器人**；另外想要人形會走路 | 使用者的觀察：**走路目前沒有好的應用場景** |
| **醫院 CSSD（真正的使用者）** | 若能做到**打包（器械包）**才是真需求 | **現階段太難**，做不到 |
| **Yang 教授（現指導）** | 沒有明確想法；**已口頭同意要簽** | 不再是阻礙（2026-08-20） |

---

## 🚀 即將要做

> **2026-08-20 依教授的 10 步驟重排。** 對應關係：1–3 已完成，主線＝**4 Pose estimation → 6 Grasp planning →（5 Motion planning）→ 7 Vision-language understanding → 8 Autonomous manipulation → 9 Human-robot collaboration → 10 Real-world validation**。
> **排序原則**：① 教授專長是影像，骨幹留在影像主線；② chatbox 落在步驟 7；③ **行走搬運降級為選配**。

### 階段一：基礎建設（官方框架遷移）
- [ ] 安裝 Isaac Lab + `unitreerobotics/unitree_sim_isaaclab`，跑通官方 `Isaac-PickPlace-Cylinder-G129-Dex3-Joint` 範例（預估：1–2 週；依賴：無）— 產出：官方 G1+Dex3 pick-place 在本機能跑
  - ⚠️ 風險：RTX 5060 Ti 8GB VRAM 偏小（官方測試機為 3080 以上）；RTX 50 系需 Isaac Sim 5.0+。若跑不動，降解析度/env 數，或借實驗室 GPU
- [ ] 評估：現有 RMPflow 手臂控制 vs unitree_sim_isaaclab 的控制方式，決定夾取方案走哪條（預估：3 天；依賴：上一項）— 產出：決策紀錄（寫入 plan-changelog）
- [ ] 把手術器械 USD 資產搬進 unitree_sim_isaaclab 場景，接上現有 YOLO 辨識（預估：1 週）— 產出：G1 面前桌上有器械且能即時辨識

### 階段二｜步驟 4：Pose Estimation（**物件的姿態，不是機器人的**）★ 影像主線的核心

> **釐清（2026-08-20）**：這裡的 pose 指**手術器械（物件）的 6D 姿態**——位置 (x,y,z) ＋ 朝向 (roll,pitch,yaw)。機器人自己的姿態由正向運動學算得出來，不需要「估」。
> 為什麼需要物件姿態：現有的 2D→3D 只給得出「器械在哪」（一個點），但要夾起來還得知道**它怎麼躺著**——刀刃朝哪、柄在哪一端、要從哪個角度下手。**位置決定去哪裡，姿態決定怎麼夾。**
- [ ] **合成資料補 6D pose 標註**：現有 Replicator pipeline 改輸出物件姿態（預估：1 週；依賴：無）— 產出：帶 pose ground truth 的資料集
- [ ] **器械 6D pose 估測**：YOLO 分割 → 姿態估測（候選做法：pose head／PnP＋關鍵點／FoundationPose 類方法，先比較再選）（預估：2–3 週）— 產出：pose 誤差可量化的模型
- [ ] **失敗案例分析**：細長件、反光、疊放、對稱器械（對稱會造成姿態多解）（預估：1 週）— 產出：論文實驗章節的第一塊
- [ ] **資產缺口**：評估 **NeRF／Meta SAM 3D → mesh → USD**（3DGS 已排除，見 dev-log 2026-08-20）（預估：1 週）— ⚠️ 工研院自述手動拉一支器械約 1 小時且需實體器械

### 階段三｜步驟 6＋5：Grasp Planning 與 Motion Planning
- [ ] **抓取姿態生成**：由 pose／點雲產生抓取候選，處理細長件與「不能夾到刃口」這類約束（預估：2–3 週；依賴：階段二）— 產出：對 ≥3 種器械能算出可行抓取
- [ ] **運動規劃接上**：沿用現有 RMPflow（或改 MoveIt 類），加碰撞檢查（預估：1–2 週）— 產出：從抓取候選到可執行軌跡
- [ ] **Dex3 實際夾取驗證**：先 scripted/teleop 驗證可夾性（器械細長是難點，可能要調姿態或擺放）（預估：2–3 週）— 產出：夾起 ≥3 種器械的成功 demo
- [ ] **分類放置迴圈**：依類別放到對應收納位置（預估：2 週）— 產出：完整分揀 demo 影片

### 階段四｜步驟 7：Vision-Language Understanding（chatbox）
- [ ] **最小可行 chatbox**：自然語言 → LLM 解析成 (動作, 物件, 目標) → **用 YOLO 分割結果做影像 grounding** → 呼叫既有 pick&place → 逐步回報狀態（預估：2 週；依賴：階段三）— 產出：打一句話機器人就動的 demo
- [ ] **指代與模糊指令**：「那支彎的」「最上面那支」「跟剛才那支一樣的」——這是**影像 grounding 的論文點**，不是語言題（預估：1–2 週）
- [ ] **量化評估**：指令成功率、grounding 準確率、失敗類型分布（預估：1 週）— 產出：論文實驗章節的第二塊
- [ ] （後續評估，不排入主線）GR00T-N／端到端 VLA 是否適用於 G1＋Dex3

### 階段五｜步驟 8＋9：自主操作與多機協作
- [ ] **全自主迴圈**：identify → localize → grasp → hand over → place → organize 一次跑完（預估：2 週）— 產出：教授指定的自主行為全數達成
- [ ] **★ 同一個指令下給多台機器人**（工研院想推的方向、教授清單第 9 項）（預估：3 週）— **從影像切入**：多視角／跨機器人的共同場景理解、指令該落到哪一台、誰看到哪一支器械 — 產出：差異化貢獻點（工研院展場的單台雙臂 demo 沒做到這件事）

### 階段六｜步驟 10：Real-World Validation（待工研院 G1 到貨，**⚠️ 採購沒把握**）
> ⚠️ 2026-08-20：工研院說要買 G1，但沒那麼有把握。**論文主體不要依賴這一段**；若沒到貨走 Plan B（用實驗室現有手臂做局部實機驗證）。
- [ ] Sim-to-real：`unitree_sim_isaaclab` 與實機同為 DDS 通訊協定，模擬程式碼可直接對接 — 這是選它當基底的關鍵理由
- [ ] 實機驗證與 sim-to-real 落差分析（預估：依到貨時間）— 產出：論文最後一塊實驗

### 階段七：論文整合
- [ ] 整合 demo：一句指令 → 辨識 → 姿態 → 抓取 → 分類放置（預估：2 週）
- [ ] 論文寫作素材整理（實驗數據、消融、影片）（預估：持續）

### 🎁 選配：行走與搬運（**降級，炫砲用**）
> **2026-08-20 決策**：教授的 10 步驟裡沒有行走、與影像無關、使用者判斷也沒有好的應用場景（CSSD 的器械多在同一區流轉）。**保留為 demo 附加項，只有主線完成且有餘裕才做。**
> **移動需求優先用「搭車」**——把機器人／手臂裝在移動平台（AMR）上，比雙足行走穩得多。展場佐證：Solomon 是 UR 手臂裝在 MiR AMR 上的複合機器人（MMR），研華也專門做 MMR 控制器。**雙足行走留給要炫的場合。**

- [ ] （選配）跑通 `unitree_rl_lab` ＋ `unitree_rl_gym` 預訓練行走 policy，讓 G1 依速度指令行走（預估：2 週）
- [ ] （選配）搬盒子行走：上半身固定持盒姿態 ＋ 行走 policy，加 payload 域隨機化 fine-tune（預估：3–4 週）
- [ ] （選配）放置到櫃子上：行走至櫃前 → 停止 → 上半身放置（預估：2 週）
---

## 📌 待處理（非本專案）

### 2026 台北國際自動化工業大展（8/19–8/20 參觀）

紀錄：[data/field-notes/2026-08-automation-taipei/](field-notes/2026-08-automation-taipei/)。照片 151 張、影片 35 段已全部判讀並回填；8/28 例會的分享稿初稿完成（FANUC 與 Solomon 的 chatbox 與語音輸入）。`career/job-matching` 與 `career/interest-tracker` 已跑過。

剩下的：
- [ ] 11 段錄音先跳過（本機無語音辨識工具；要處理時用 iPhone 轉錄或裝 whisper.cpp）
- [ ] 補問各家「徵什麼職能」——現場兩天都沒問到，改看 104／官網職缺
