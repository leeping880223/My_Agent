# 目標職缺與 requirement

由 job-matching 維護。最後更新：2026-08-20（首次建立，依 2026 自動化展兩天所見）。

> **需求來源標記**：**（官網）**＝公司徵才頁／新聞可查證；**（業界通用）**＝具身智能／機器人 AI 職缺的共通要求，取自 2026-08 的公開職缺整理，非特定公司 JD；**（展場推定）**＝由該公司在 2026 自動化展公開的技術棧反推。
> ⚠️ 尚未取得任何一家的正式 JD 原文。投履歷前要用 104／官網逐項核對。

---

## T1（主目標）具身智能／機器人 AI 演算法工程師

**對象**：達明機器人（TM Xplore I 人形團隊）、台達電（具身智能雙臂協作平台）、Solomon 所羅門

**為什麼是主目標**：技術棧與碩論幾乎重疊；達明與台達都是大型上市公司；三家都與 NVIDIA 有合作關係。

| # | Requirement | 來源 |
|---|---|---|
| 1 | Python 熟練 | （業界通用） |
| 2 | **C++ 工程能力** | （業界通用） |
| 3 | PyTorch | （業界通用） |
| 4 | **ROS2** | （業界通用；研華的 Robot Control Package 也整包基於 ROS2） |
| 5 | Ubuntu／Linux 開發環境 | （業界通用） |
| 6 | **機器人模擬平台：Isaac Sim／Isaac Lab**（或 MuJoCo／Gazebo／PyBullet） | （業界通用）＋達明公開表示採用 Isaac Sim 做數位孿生驗證（官網／新聞） |
| 7 | **VLA（Vision-Language-Action）、模仿學習、強化學習** | （業界通用） |
| 8 | 了解主流具身智能模型（RDT、π0、Diffusion Policy、GR00T-N 等） | （業界通用） |
| 9 | 合成資料生成／sim-to-real | （展場推定：達明用 GR00T Blueprint 生成合成資料；研華 AI Factory 第 4 階段） |
| 10 | 機器視覺（偵測／分割／6D pose） | （展場推定：達明 TM AI Vision；Solomon 3D 視覺取放） |

---

## T2（次目標）機器人視覺／3D 視覺工程師

**對象**：Solomon、達明（TM AI Vision）、EverFocus、大都電子這類視覺整合商

| # | Requirement | 來源 |
|---|---|---|
| 1 | 影像偵測／分割模型訓練與部署（YOLO 類） | （展場推定） |
| 2 | **3D 視覺：點雲、6D pose、bin picking** | （展場推定：Solomon 的核心產品） |
| 3 | 手眼標定、相機／鏡頭／光源選型 | （展場推定：EverFocus、大都電子的產品線） |
| 4 | 邊緣端推論最佳化（Jetson、TensorRT） | （展場推定：研華、EverFocus 都在 edge 跑） |
| 5 | 與手臂整合（取放流程、座標轉換） | （展場推定） |

---

## T3（備選）Edge AI／機器人應用工程師（IPC 廠）

**對象**：研華（NVIDIA Elite Partner）、磐儀 ARBOR

⚠️ **注意**：IPC 廠的職缺可能偏硬體整合／驅動，也可能是 Edge AI 應用，差別很大。**看到職缺描述再判斷**，不要一律當成同一類。

| # | Requirement | 來源 |
|---|---|---|
| 1 | Jetson／x86 邊緣平台部署 | （展場：研華 MIC-760、NVIDIA Certified 平台） |
| 2 | ROS2、DDS（FastDDS／CycloneDDS） | （展場：研華 Robot Control Package） |
| 3 | NAV2／SLAM／MoveIt2 | （展場：研華 Robot Control Package） |
| 4 | Omniverse／數位孿生 | （展場：研華 Digital Twin 六階段） |
| 5 | 硬體整合、驅動、工控通訊 | （展場推定；**這項與使用者的定位不合，要留意**） |

---

## T4（觀察名單）機器人新創／整合商

**對象**：Holon Robotics（NVIDIA Inception，AI 生成機器人程式）、至盛科技（Unitree 台灣代理）、台智寶（上緯智聯，本土人形＋四足）

- 特徵：規模小、變動大，但**技能重疊度最高、進入門檻相對低**，且至盛直接碰 Unitree G1（＝碩論用的機器人）。
- 建議定位：**觀察與人脈**，不是第一志願；實習或專案合作是比較合適的接觸方式。

---

## 待補（下次跑 job-matching 前要做）

- ⬜ 取得至少 3 份**正式 JD 原文**（104／公司官網），把上面的「業界通用／展場推定」換成真實條件
- ⬜ 確認各家是否有**碩士應屆**職缺與投遞時程
