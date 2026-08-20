# 計畫調整紀錄

由 plan-adjuster 維護，記錄 goals.md 的每次變更。

| 日期 | 改變內容 | 原因 |
|---|---|---|
| 2026-07-28 | **論文題目整個換掉**：原本的 RL 題目 → ITRI 手術器械專案，教授提議定名為 *Autonomous Surgical Instrument Manipulation Using Vision-Language-Action Models in Isaac Lab*（長版含 Task Planning 與 Humanoid Manipulation）。教授給出 10 步驟進程並指定聚焦 4–10。 | 原 RL 題目不可行：收集後發現 **action data 是 perception data 的 4 倍以上，且 perception data 不規則**，無法做強化學習。轉向 ITRI 專案後可用 Isaac Sim／Isaac Lab／GR00T，且同時有模擬與實機。（此變更 2026-08-20 才補寫進檔案，先前只存在對話中） |
| 2026-07-28 | **指導安排變動（未完成）**：Basanta 教授表示願意指導，前提是 Yang 教授同意；Yang 教授先前表示沒有 bandwidth 接新專案。 | 新方向與現有實驗室的主軸差異大。⬜ 待把 Yang 教授的同意走完。 |
| 2026-08-20 | **方向確認（非變更）**：自動化展兩天所見證實 VLA／語言介面是產業共識（台達 大腦 VLM/LLM＋小腦 EtherCAT、FANUC chatbox、達明 GR00T、Solomon 語言指令人形取物），與教授 7/28 提的方向一致。同時記下三方期待落差（教授無行走／工研院要走路但無場景／醫院真需求是打包）。 | 展場實地觀察，詳見 [field-notes](field-notes/2026-08-automation-taipei/README.md)。 |
| 2026-08-20 | **3DGS 從資產生成方案中移除**，改評估 NeRF／Meta SAM 3D → mesh → USD。 | 3DGS 輸出點雲、無 mesh 即無 collision，Isaac Sim 用不了。詳見 [dev-log](dev-log/2026-08-20-3dgs-no-collision.md)。 |
| 2026-08-20 | **指導安排的障礙解除**：Yang 教授口頭同意要簽，Basanta 教授的指導前提達成，只剩行政簽署。同時定調**論文重心維持在影像／視覺主線**（Basanta 專長是影像），VLA 作為串接介面而非取代影像。另：免寫 code 的圖形化編程改判為加分項，移出主線。 | 使用者 2026-08-20 告知。 |
| 2026-08-20 | **goals.md 階段全面重排**（plan-adjuster）：改依教授的 10 步驟編排——階段二＝Pose estimation、階段三＝Grasp＋Motion planning、階段四＝Vision-language understanding（chatbox）、階段五＝自主操作＋**同一指令多機協作**、階段六＝實機驗證。**原階段三「行走與搬運」整段降級為選配（demo 炫砲用）**，並註明移動需求優先用「搭車」（機器人裝在 AMR 上）而非雙足行走。 | 教授的 10 步驟沒有行走、Basanta 專長是影像、使用者判斷行走沒有好的應用場景；chatbox 則是 2026 自動化展所見（FANUC／Solomon／台達）且正好落在步驟 7。使用者 2026-08-20 拍板：「行走可能就當另一個外加的炫砲用的，現在還是搭車比較穩」。 |
