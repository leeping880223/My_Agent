# 論文庫總覽

已讀論文清單。每篇論文一個資料夾（從 [_template](_template/) 複製），資料夾內有詳細重點、理解程度、補充教學與投影片。

新增論文請使用 `qa-check-knowhow` skill，命名格式：`<年份>-<第一作者>-<簡短題名>`。論文原始檔統一存為該資料夾內的 `paper.pdf`。

## 已讀論文

| 論文 | 重點概要 | 資料夾 |
|---|---|---|
| Riemannian Motion Policies (Ratliff et al., 2018) | 加速度策略＋Riemannian 度量的模組化運動生成框架；多策略經 pullback/加權合成到 C-space 且證明最優，是 Isaac Sim RMPflow 的理論基礎 | [2018-ratliff-rmp](2018-ratliff-rmp/) |
| RMPflow: A Computational Graph for Automatic Motion Policy Generation (Cheng et al., 2019) | 把 RMP 擴成樹狀計算圖：每個控制週期一次 forward（傳狀態）＋一次 backward（傳力與度量）O(K) 算出關節加速度；引入速度相關度量與曲率項，並給出穩定性與座標無關性的證明。Isaac Sim Lula RMPflow 實作的就是這篇 | [2019-cheng-rmpflow](2019-cheng-rmpflow/) |

## 待讀清單

| 論文 | 為什麼要讀／優先序 | 檔案位置 |
|---|---|---|
| cuRobo（NVIDIA，2023，62 頁） | **下一篇**。2026-08-18 決定先讀 RMPflow 再讀它，理由：RMPflow 是 2018 RMP 的正統續作、記憶正熱且有 Isaac Sim 實操可掛鉤；cuRobo 幾乎不依賴 RMP 的數學，但**它是 [goals.md](../goals.md) 階段一那條「現有 RMPflow 手臂控制 vs unitree_sim_isaaclab 控制方式」決策的關鍵輸入**（GPU 平行的 collision-free IK 與軌跡最佳化，是 Isaac Lab 生態裡 RMPflow 的主要替代方案）。讀完 RMPflow 再讀它，可以直接對比「反應式策略合成」vs「全域最佳化」兩條路線 | `~/Downloads/cuRobo.pdf`（**尚未收進 paper-library**，開跑 qa-check-knowhow 時再複製） |

**提前判斷**：如果哪天變成「這週就要跑 unitree_sim_isaaclab、當場要決定控制方案」，就把 cuRobo 提前到 RMPflow 前面——這是唯一該調換順序的情況。
