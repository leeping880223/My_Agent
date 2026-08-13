---
name: weekly-report
description: 讀取 data/goals.md 和 data/dev-log/，產出兩個檔案到 data/weekly/：一份 PPT 和一份 MD，完整說明本週完成的任務。
---

# weekly-report：週報產出

## 目的

每週把進度整理成兩種格式：MD 供快速閱讀與存檔，PPT 供會議報告使用。

## 執行步驟

1. **蒐集本週素材**
   - 讀取 `data/goals.md`：找出本週新完成的任務（「已完成」區的新項目）與進行中任務的狀態。
   - 讀取 `data/dev-log/`：找出本週日期的踩坑紀錄。
   - 讀取 `data/plan-changelog.md`：確認本週是否有計畫調整。
   - 向使用者補問：有沒有沒記錄到的本週工作？下週的重點是什麼？

2. **組織週報內容**（兩種格式共用同一份內容）
   - 本週完成的任務：每項附具體成果與產出物
   - 遇到的問題與解法：取自 dev-log（嘗試 → 失敗原因 → 改用方案）
   - 計畫變更：若有，說明改了什麼與原因
   - 下週計畫：取自 goals.md「即將要做」區的優先項目

3. **產出兩個檔案到 `data/weekly/`**
   - 命名以本週週一日期為準：
     - `YYYY-MM-DD-weekly.md`：Markdown 版本，完整詳細。
     - `YYYY-MM-DD-weekly.pptx`：投影片版本（使用 pptx skill 製作），每個主題一頁、重點條列，適合口頭報告。

4. **收尾**
   - 向使用者展示週報摘要，確認內容無誤。
   - 依 CLAUDE.md 流程，詢問是否執行 `dev-logger` 與 `interest-tracker`。
