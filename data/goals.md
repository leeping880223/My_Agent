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
- [ ] 8/20 依現場捕捉清單蒐集（每家：定位／demo／技術棧／有無用 NVIDIA／徵什麼職能／拍照）
- [ ] 錄音與照片放進 `media/`，回填紀錄檔（把「（網查）」換成第一手內容）
- [ ] **實習分享報告**：挑 3–5 家產出心得＋重點資訊，**2026-08-28（五）例會**（倒推時程見紀錄檔）
- [ ] 展後跑 `career/job-matching`：把有興趣的公司／職缺寫進 `career-plan/job-targets.md`，做技能差距分析
- [ ] 跑 `career/interest-tracker` 記錄逛展感受

**已浮現、值得追的三家**（都與 G1 論文直接相關）：至盛科技（Unitree 台灣代理／整合）、台智寶（上緯，本土人形＋四足，正在組生態系）、Solomon（3D 視覺 bin picking，正面對上手術器械夾取問題）。
