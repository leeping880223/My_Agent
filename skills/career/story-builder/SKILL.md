---
name: story-builder
description: 讀取 goals.md、dev-log/、plan-changelog.md、career-plan/changelog.md、profile/task-feelings.md，把研究和開發經歷（包含轉向的決策過程）轉換成 STAR 格式的面試故事素材。
---

# story-builder：STAR 面試故事素材

## 目的

把日常累積的研究／開發紀錄轉換成面試可用的故事。轉向與失敗的決策過程往往是最有價值的素材（展現判斷力與韌性），不要只挑成功案例。

## 執行步驟

1. **讀取所有素材來源**
   - `data/goals.md`：完成過哪些任務、目標的演變。
   - `data/dev-log/`：踩坑與解決過程（失敗 → 分析 → 替代方案 = 現成的故事骨架）。
   - `data/plan-changelog.md`：計畫轉向的時間點與原因。
   - `data/career-plan/changelog.md`：職涯目標的轉變與原因。
   - `data/profile/task-feelings.md`：使用者對各任務的真實感受（讓故事講起來自然、有個人動機）。

2. **確認目標職缺（若有）**
   - 詢問使用者這批故事要對準什麼職缺／面試，可參考 `data/career-plan/job-targets.md`，讓故事重點對齊該職缺看重的能力。

3. **挑選故事候選**
   - 從素材中找出符合以下任一類型的事件：
     - 解決困難的技術問題（dev-log 中的大坑）
     - 重大轉向決策（plan-changelog、career-plan/changelog 中的變更）
     - 從零建立某個東西（goals.md 的里程碑）
     - 與他人協作或說服他人（領導回饋觸發的調整）
   - 向使用者確認事件細節、補問缺少的資訊（規模、影響、數字）。

4. **轉換成 STAR 格式**
   - 每個故事寫成：
     - **S（Situation）**：背景與限制條件
     - **T（Task）**：使用者的職責與目標
     - **A（Action）**：具體做了什麼——包含決策過程：考慮過哪些選項、為何選這個、為何放棄那個（取自 changelog 與 dev-log）
     - **R（Result）**：可量化的成果 + 學到什麼
   - 每個故事附上「適用的面試問題」標籤（如：講一個失敗經驗、講一次和主管意見不合）。

5. **產出**
   - 將故事素材整理成文件交給使用者（建議存放位置由使用者決定，例如 `data/career-plan/` 底下）。
   - 提醒使用者：素材要口語化練習過才能上場，可搭配 `4.review` 的「說」階段模式演練。
