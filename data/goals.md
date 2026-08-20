# 長期計畫表

由 goal-planner 建立、plan-adjuster 調整。任務完成後從「即將要做」移到「已完成」。

## 專案：G1 手術器械分揀 + 搬運（碩士論文，與工研院合作）

**目標**：Unitree G1 在 Isaac Sim/Lab 中（1）辨識手術器械並用 Dex3 三爪手實體夾取、分類放置；（2）拿著盒子行走、放到櫃子上。模擬為主，畢業需上實機（工研院採購中）。

**Repo**：https://github.com/leeping880223/Isaac-sim

## 📌 論文題目與方向（2026-07-28 與 Basanta 教授確認；2026-08-20 補上三方期待）

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

### 指導安排（2026-08-20 更新：障礙已排除）

- **Basanta 教授願意指導**：「I am fine with it」「If he agrees, I can supervise you」
- **Yang 教授已口頭同意要簽**（使用者 2026-08-20 告知）→ **前提條件達成，這關過了**
- ⬜ 只剩把簽名的行政程序走完

### ⚠️ Basanta 教授的專長是影像（2026-08-20 補，影響選題重心）

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

### 💬 chatbox 介面（想法來源：2026 台北國際自動化工業大展，8/19–8/20）

**這一項不是教授指定的，是這次逛展看到、判斷值得加進來的**（詳見 [field-notes](field-notes/2026-08-automation-taipei/README.md)）。

**展場上的三個現成範例**：

| 來源 | 做法 | 可借鑑的地方 |
|---|---|---|
| **FANUC** Physical AI Demo | 右側就是一個 chatbox：打「請寫 DRAGON」→ 回「先確認棋盤與托盤狀態…」→「開始寫…」→「完成！」；程式碼是 LLM 呼叫既有的 `pick_letter()`、`find_specific_word_move()` | **LLM 產生的是「呼叫既有 API 的高階指令」，不是關節角**。而且**逐步回報狀態**，使用者知道機器人在想什麼 |
| **Solomon**（M400） | 打「找到葡萄汁，走過去拿起來，走回起始位置拿給我」→ 回「找到了，clear grape juice bottle 大約在正前方 5 公尺」→ 人形執行 | **回覆裡把「它認為自己看到什麼」講出來**，這是影像 grounding 的可視化 |
| **台達 × NVIDIA** | 架構圖：大腦＝VLM｜LLM｜GPU，小腦＝EtherCAT｜工控 | 分層方式可直接照抄當論文的系統架構圖 |

**★ 需求來源（2026-08-20 補，這條最關鍵）**：**工研院實習主管明講他們目前較缺 chatbox／VLA 這一塊**——使用者是因此才特別注意這個主題。也就是說，這不只是「展場看到覺得酷」，而是**合作單位講出來的缺口**。

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

### 三方期待對照（2026-08-20 補）

| 誰 | 想要什麼 | 落差／風險 |
|---|---|---|
| **Basanta 教授** | VLA ＋ 任務規劃 ＋ 自主操作（10 步驟的 4–10）；**清單裡沒有「行走搬運」** | 與 goals.md 現行的階段三（行走、搬盒）對不上 |
| **工研院（ITRI）** | 推 **VLA 應用**：可下指令，**未來同一個指令可以下給多台機器人**；另外想要人形會走路 | 使用者的觀察：**走路目前沒有好的應用場景** |
| **醫院 CSSD（真正的使用者）** | 若能做到**打包（器械包）**才是真需求 | **現階段太難**，做不到 |
| **Yang 教授（現指導）** | 沒有明確想法；**已口頭同意要簽** | 不再是阻礙（2026-08-20） |

### ⬜ 由此產生的待決策

1. **行走搬運（現行階段三）要不要留？**
   - 支持留：工研院想要、是 G1 這個平台的賣點、與目標 2（搬盒行走）一致
   - 支持砍：教授的 10 步驟沒有它、沒有好的應用場景、CSSD 的器械是在同一個房間內流轉、投入成本高（RL policy fine-tune 3–4 週起跳）
   - 折衷：**降級成 demo 附加項**，論文主體放 4–10；或改成「同一指令下給多台機器人」的多機協作（正好對上工研院想推的東西，也對上教授清單的第 9 項 Human-robot collaboration）
2. **「同一個指令給多台機器人」值得當成差異化的貢獻點嗎？**——這是工研院想推、教授清單有（#9）、而工研院展場 demo（單台雙臂）沒做到的地方
3. **打包（packing）**：現在做不到，但值得在論文的「未來工作」寫清楚，並說明為什麼難（軟性材料、摺疊、無剛體假設）

---

## ✅ 已完成

- [x] **（教授步驟 1 Synthetic data generation）** 手術器械合成資料 pipeline（14 種 USD → Replicator 拍照 → YOLO seg 格式）— mAP50 ~0.9
- [x] **（教授步驟 2 Instrument segmentation ＋ 3 3D localization）** Isaac Sim 即時辨識 + 2D→3D 座標轉換（`inference/yolo_isaac_final.py`）
- [x] G1 右手臂 RMPflow reach demo — 手刻 URDF/RMPflow 設定，YOLO 驅動伸手到器械位置（限制：rubber_hand 不能夾、pelvis 釘死不能走）

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

### 階段六｜步驟 10：Real-World Validation（待工研院 G1 到貨）
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

### 2026 台北國際自動化工業大展（8/19 下午、8/20 全天）— 進行中

紀錄位置：[data/field-notes/2026-08-automation-taipei/](field-notes/2026-08-automation-taipei/)
（2026-08-19 新增 `data/field-notes/` 這一類資料夾，用途見 [field-notes/README.md](field-notes/README.md)，CLAUDE.md 第 2 節已同步）

- [x] 建立紀錄檔，寫入 8/19 已看的公司與 8/20 待看清單
- [x] 8/19 素材回填：131 張照片＋23 段影片已全部判讀並寫入紀錄檔；完整議程已補齊
- [ ] **11 段錄音尚未轉逐字稿**（本機無語音辨識工具，待決定作法）
- [x] 8/20 二次參觀完成，素材（20 照片＋12 影片）已判讀並寫入紀錄檔
- [ ] 錄音 11 段**先跳過**（使用者 2026-08-20 決定）；要處理時用 iPhone 轉錄或裝 whisper.cpp
- [ ] 展後補問「徵什麼職能」（兩天現場都沒問到）——改看 104／官網職缺
- [ ] ~~3DGS 試用~~ **已下修**：3DGS 是點雲、無 collision，Isaac Sim 用不了（見 [dev-log 2026-08-20](dev-log/2026-08-20-3dgs-no-collision.md)）。改評估 **NeRF／Meta SAM 3D → mesh → USD**；工研院自述手動拉一支器械約 1 小時且需實體器械
- [ ] **實習分享報告**：挑 3–5 家產出心得＋重點資訊，**2026-08-28（五）例會**（倒推時程見紀錄檔）
- [ ] 展後跑 `career/job-matching`：把有興趣的公司／職缺寫進 `career-plan/job-targets.md`，做技能差距分析
- [ ] 跑 `career/interest-tracker` 記錄逛展感受

### ⚠️ 待決策：論文方向可能從「視覺」轉向「VLA ＋ chatbox」（2026-08-20 浮現）

使用者原話：「本來想做變焦鏡頭相關的，像是索羅門這樣，但工研院可能比較想要用 VLA、並且是可以用 chatbox demo 這樣。」

- **最優先待辦**：⬜ **工研院攤位當場在做雙臂人形「手術器械分揀」demo，與本論文題目重疊**——要問清楚是哪個所、用什麼方法、**與本論文的分工與差異化**。這件事比選哪條路更急。
- ⬜ 問工研院窗口／指導教授：期待的是視覺路線還是 VLA／chatbox 路線？
- ⬜ 若走 chatbox：先做最小可行版（自然語言 → 既有 pick&place API），不要一開始就導 GR00T／端到端 VLA
- ⬜ 決定後更新本檔階段規劃，並在 `plan-changelog.md` 記一筆
- 完整對照（兩條路的資產／缺口／風險）見紀錄檔「論文方向的轉折點」一節

**Day 1 結論**：人形機器人在台灣已是完整供應鏈（上銀／富田 關節 → 研華／磐儀 控制器 → 達明／台智寶／至盛 整機 → Solomon／新代 應用），且共同方法論是**模擬先行＋合成資料**。
- 達明 TM Xplore I 明講用 **Isaac Sim ＋ GR00T VLA ＋ 合成資料**；研華 AI Factory 六階段第 ④ 階段就是合成資料訓練；Solomon 現場展**語言指令 → 人形走過去取物帶回**（＝本論文目標 1＋2 的合體）。
- ⚠️ **對論文的待辦**：工研院 3DGS 拍照建模可能可生成手術器械資產（但高反光金屬是已知弱點）；先臨三維現場證實金屬件要**噴顯影劑＋貼標記點**才掃得起來。細節見紀錄檔「對 G1 論文的直接影響」。

**Day 2 補充**：展場共識是 **LLM／VLM 當大腦、傳統視覺與控制當小腦**（台達投影片寫得最白）。現有的 YOLO＋RMPflow＋Dex3 抓取正是「小腦」，上面加一層對話介面即可，A 路線的投入不會白費。

**★ 角色定位（2026-08-20 使用者自述，影響後續所有取捨）**：
> 工研院目前給我的任務，我比較感覺像是**公司（工研院）買了設備，而我是他們的應用商**。硬體規格不是我可以控制的——KUKA 的手臂、研華的 IPC，他們買什麼我們就用什麼。

- 因此：**硬體／零組件情報一律降低優先度**（上銀、富田、IPC 廠商等，知道即可）；**大腦層（辨識、決策、任務規劃、對話介面）才是要投入的地方**。
- 8/20 刻意沒去研華、Solomon、磐儀、利凌、KUKA 攤位，就是這個判斷下的取捨，不是漏看。
- ⚠️ 但要記得：應用端**不決定硬體，卻要為硬體限制負責**（Dex3 夾不夾得起細長器械、G1 算力）。
- **★ 小腦也要會，只是不做創新（2026-08-20 使用者補充）**：主管**沒有提供現成的 code 或 open source 連結**讓人照著做，所以底層控制（小腦）的資源要自己去搜、自己拼起來，**基本能力必須具備**。分工是：**小腦＝找得到、接得起來、能 debug；大腦＝創新與論文貢獻所在。**
- **★ 硬體策略：用手上現有的資源拼出來（2026-08-20 拍板）**：**不去找更好的相機或更多硬體資源**，重點是把手上已有的東西湊出可行的系統。理由是問題比較單純、不用想得太複雜。→ 因此本專案**不排入任何「採購／評估更好相機」的任務**；遇到硬體限制先想「現有條件下怎麼繞過」。

**★ 落地場域＝醫院 CSSD（消毒供應中心）**：達明「不用寫 code 的流程式編程」讓使用者想到——CSSD 現場操作的是護理／技術人員而非工程師，**「誰來設定這台機器」是真實的產品問題**，可作為論文應用價值的論述之一。
