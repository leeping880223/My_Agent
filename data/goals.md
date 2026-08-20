# 長期計畫表

由 goal-planner 建立、plan-adjuster 調整。任務完成後從「即將要做」移到「已完成」。

## 專案：G1 手術器械分揀 + 搬運（碩士論文，與工研院合作）

**目標**：Unitree G1 在 Isaac Sim/Lab 中（1）辨識手術器械並用 Dex3 三爪手實體夾取、分類放置；（2）拿著盒子行走、放到櫃子上。模擬為主，畢業需上實機（工研院採購中）。

**Repo**：https://github.com/leeping880223/Isaac-sim

## ✅ 已完成

- [x] 手術器械合成資料 pipeline（14 種 USD → Replicator 拍照 → YOLO seg 格式）— mAP50 ~0.9
- [x] Isaac Sim 即時辨識 + 2D→3D 座標轉換（`inference/yolo_isaac_final.py`）
- [x] G1 右手臂 RMPflow reach demo — 手刻 URDF/RMPflow 設定，YOLO 驅動伸手到器械位置（限制：rubber_hand 不能夾、pelvis 釘死不能走）

## 🚀 即將要做

### 階段一：官方框架遷移（基礎建設）
- [ ] 安裝 Isaac Lab + `unitreerobotics/unitree_sim_isaaclab`，跑通官方 `Isaac-PickPlace-Cylinder-G129-Dex3-Joint` 範例（預估：1–2 週；依賴：無）— 產出：官方 G1+Dex3 pick-place 在本機能跑
  - ⚠️ 風險：RTX 5060 Ti 8GB VRAM 偏小（官方測試機為 3080 以上）；RTX 50 系需 Isaac Sim 5.0+。若跑不動，降解析度/env 數，或借實驗室 GPU
- [ ] 評估：現有 RMPflow 手臂控制 vs unitree_sim_isaaclab 的控制方式，決定夾取方案走哪條（預估：3 天；依賴：上一項）— 產出：決策紀錄（寫入 plan-changelog）

### 階段二：手術器械夾取與分揀（目標 1）
- [ ] 把手術器械 USD 資產搬進 unitree_sim_isaaclab 場景，接上 YOLO 辨識（預估：1 週）— 產出：G1 面前桌上有器械且能即時辨識
- [ ] Dex3 夾取單一器械（先 scripted/teleop 驗證可夾性，器械細長是難點，可能需調抓取姿態或器械擺放）（預估：2–3 週）— 產出：夾起 ≥3 種器械的成功 demo
- [ ] 分類放置：依 YOLO 類別把器械放到對應收納位置，完成 sorting 迴圈（預估：2 週；依賴：上一項）— 產出：完整分揀 demo 影片

### 階段三：行走與搬運（目標 2）
- [ ] 跑通 `unitreerobotics/unitree_rl_lab`（官方 IsaacLab RL，支援 G1-29dof）＋ `unitree_rl_gym` 預訓練行走 policy，讓 G1 在場景中依速度指令行走（預估：2 週；依賴：階段一）— 產出：G1 行走 demo
- [ ] 搬盒子行走：上半身固定持盒姿態 + 行走 policy，加 payload 域隨機化 fine-tune 提升穩定度（RL 基礎正好用上）（預估：3–4 週；依賴：上一項）— 產出：持盒行走不倒的 policy
- [ ] 放置到櫃子上：行走至櫃前 → 停止 → 上半身放置動作（預估：2 週；依賴：上一項）— 產出：walk-carry-place 完整 demo

### 階段四：整合與論文
- [ ] 整合 demo：辨識 → 分揀 → 搬運 → 放置 完整流程（預估：2 週；依賴：階段二、三）
- [ ] 論文寫作素材整理（實驗數據、消融、影片）（預估：持續）

### 後期（待工研院 G1 到貨）
- [ ] Sim-to-real：unitree_sim_isaaclab 用與實機相同的 DDS 通訊協定，模擬程式碼可直接對接實機 — 這是選它當基底的關鍵理由

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
- [ ] 3DGS 試用（密語 AUTO2026，**2026-09-05 截止**）
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
