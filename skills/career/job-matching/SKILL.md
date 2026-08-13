---
name: job-matching
description: 讀取 profile/skills.md 和 career-plan/，比對目前技能與目標職缺 requirement，給出差距分析與補強方向，或建議調整職業目標。技能有變化時更新 skills.md；職涯目標改變時寫入 career-plan/changelog.md 並更新 current-plan.md。
---

# job-matching：技能與職缺差距分析

## 目的

回答兩個問題：「以目前的技能，離目標職缺還差多少？」「該補強，還是該調整目標？」

## 執行步驟

1. **讀取現況**
   - `data/profile/skills.md`：目前技能與程度。
   - `data/career-plan/current-plan.md`：目前的職涯規劃。
   - `data/career-plan/job-targets.md`：目標職缺與 requirement。
   - `data/profile/interests.md`（輔助）：性向分析，用於判斷目標是否符合使用者特質。

2. **更新技能現況**
   - 詢問使用者最近是否有新技能或程度變化（新專案、新學的工具、leetcode-training 的進展）。
   - 有變化就更新 `data/profile/skills.md`。

3. **差距分析**
   - 逐一比對每個目標職缺的 requirement 與現有技能，輸出表格：

     | Requirement | 目前程度 | 差距 | 補強方式 | 預估時間 |
     |---|---|---|---|---|

   - 差距分級：`已滿足`／`小差距`（短期可補）／`大差距`（需數月投入）。

4. **給出建議（二擇一或並行）**
   - **補強路線**：差距集中且可補 → 給出具體補強計畫（學什麼、按什麼順序、用什麼專案練），並建議用 `goal-planner` 把補強計畫排進 `data/goals.md`。
   - **調整目標**：差距過大、或 interests.md 顯示目標與性向不合 → 建議更符合現況的職缺方向，說明理由。

5. **職涯目標改變時的記錄**（使用者決定調整目標才執行）
   - 在 `data/career-plan/changelog.md` 追加：

     | 日期 | 變更內容 | 原因 |
     |---|---|---|

   - 更新 `data/career-plan/current-plan.md` 為新的規劃。
   - 若有新目標職缺，更新 `data/career-plan/job-targets.md`。

6. **收尾**
   - 摘要：目前最接近的職缺、最關鍵的差距、建議的下一步行動。
