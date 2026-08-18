# 論文庫總覽

已讀論文清單。每篇論文一個資料夾（從 [_template](_template/) 複製），資料夾內有詳細重點、理解程度、補充教學與投影片。

新增論文請使用 `qa-check-knowhow` skill，命名格式：`<年份>-<第一作者>-<簡短題名>`。論文原始檔統一存為該資料夾內的 `paper.pdf`。

## 已讀論文

| 論文 | 重點概要 | 資料夾 |
|---|---|---|
| Riemannian Motion Policies (Ratliff et al., 2018) | 加速度策略＋Riemannian 度量的模組化運動生成框架；多策略經 pullback/加權合成到 C-space 且證明最優，是 Isaac Sim RMPflow 的理論基礎 | [2018-ratliff-rmp](2018-ratliff-rmp/) |
| RMPflow: A Computational Graph for Automatic Motion Policy Generation (Cheng et al., 2019) | 把 RMP 擴成樹狀計算圖：每個控制週期一次 forward（傳狀態）＋一次 backward（傳力與度量）O(K) 算出關節加速度；引入速度相關度量與曲率項，並給出穩定性與座標無關性的證明。Isaac Sim Lula RMPflow 實作的就是這篇 | [2019-cheng-rmpflow](2019-cheng-rmpflow/) |
