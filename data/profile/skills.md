# 技能清單

持續更新。程度等級：`入門`／`熟悉`／`精通`；`⬜ 待確認`＝ job-matching 推測但尚未跟使用者核實。
最後更新：2026-08-20（job-matching）。
由 goal-planner、job-matching、leetcode-training 等 skill 讀取與更新。

## 程式語言

| 技能 | 程度 | 備註（專案經驗、最後使用時間） |
|---|---|---|
| Python | 熟悉 | Isaac Sim 腳本、YOLO 訓練 pipeline（2026-08 使用中） |
| C++ | ⬜ 待確認 | 具身智能職缺的共通要求，需確認目前程度 |

## 框架與工具

| 技能 | 程度 | 備註 |
|---|---|---|
| NVIDIA Isaac Sim | 熟悉 | Replicator 合成資料、USD 場景組裝、相機/光照除錯（Isaac-sim repo，2026-08） |
| YOLO (ultralytics) | 熟悉 | segmentation 訓練到 mAP50 ~0.9、即時推論整合 |
| RMPflow / Lula | 入門–熟悉 | 為 G1 手刻 URDF + RMPflow 設定（內建不支援 G1） |
| Blender | 入門 | STL → USD 模型前處理（擺正、縮放） |
| Isaac Lab | 未接觸 | G1 專案階段一要學 |
| 強化學習（RL） | 入門 | 有基礎（課程/概念），沒從頭訓練過機器人 policy |
| Git / GitHub | 入門 | 2026-08 起使用 gh CLI |
| PyTorch | ⬜ 待確認（推測入門） | 透過 ultralytics 訓練 YOLO，但是否自己寫過訓練迴圈／模型待確認 |
| ROS2 | ⬜ 待確認（推測未接觸） | 業界共通要求；研華、Solomon、達明的整合都在 ROS2 上 |
| Ubuntu / Linux | 熟悉 | 日常開發環境 Ubuntu 24.04 |
| LLM／VLA／具身智能模型 | 未接觸 | 論文階段四要用（GR00T-N、π0、Diffusion Policy 等只需先了解） |

## 領域知識

| 技能 | 程度 | 備註 |
|---|---|---|
| 機器人模擬（humanoid） | 入門–熟悉 | G1 關節結構、floating-base 物理、URDF/USD |
| 電腦視覺（偵測/分割） | 熟悉 | 合成資料生成 + 2D→3D 座標轉換 |
| **合成資料生成（Replicator）** | 熟悉 | 14 種器械 USD → 自動拍照標註 → 訓到 mAP50 ~0.9。**這項在市場上相對稀缺**（達明用 GR00T Blueprint 做同一件事、研華 AI Factory 第 4 階段就是它） |
| 6D pose estimation | 未接觸 | 論文階段二的核心，也是 T1／T2 職缺的共同要求 |
| 邊緣端部署（Jetson／TensorRT） | 未接觸 | T2／T3 職缺要求；目前專案不碰（硬體由工研院決定） |
| 人形機器人 locomotion RL | 未接觸 | 原階段三，2026-08-20 已**降級為選配**（行走搬運不在論文主線）；短期不補 |

## 軟實力

| 技能 | 程度 | 備註 |
|---|---|---|
| 技術文件撰寫 | 熟悉 | Isaac-sim repo 的 README／踩坑紀錄品質高 |
| 在沒有現成 code 的條件下自己接系統 | 熟悉 | 工研院不給 code，小腦（底層控制）資源全靠自己搜尋與整合——**面試時是好故事** |
| 系統分層與可遷移性設計 | 入門 | 論文採 PoC 定位，通用層與平台相依層分離（2026-08 起實作） |
| AI 協作／agent 工作流設計 | 入門–熟悉 | 自建個人 agent 系統（skills + data 分層），用於研究、開發、職涯管理 |
