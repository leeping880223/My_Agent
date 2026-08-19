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

- [ ] **自動化展見聞記錄**（2026-08-18 參觀，尚未記錄）— 使用者表示有東西要記錄，換聊天室後處理。
  - ⚠️ **目前 `data/` 沒有存放「外部見聞／展覽情報」的地方**。內容出來之後再依性質分流：新技術或現成方案 → `dev-log/` 或跑 `develop/newtech-searching`；影響技術路線 → 本檔＋`plan-changelog.md`；職缺或產業線索 → `career-plan/job-targets.md`；個人感受 → `profile/task-feelings.md`。若發現這些都不合適，就是該新增一類資料夾的訊號，屆時一併更新 CLAUDE.md 第 2 節。
