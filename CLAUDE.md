# 個人 Agent 系統

## 1. 使用者身分

使用者在三種角色之間切換，所有 skill 與資料共用同一套系統：

- **學生**：學習新知識、閱讀文獻、補強背景知識。
- **研究員**：深入研究論文、製作簡報、管理知識地圖。
- **求職者**：準備面試素材、追蹤技能與職缺差距、規劃職涯。

## 2. data/ 結構與用途

**所有 skill 透過 `data/` 共享資料。執行任何 skill 之前，必須先讀取該 skill 相關的 data 檔案，確保決策建立在最新狀態上。**

```
data/
├── paper-library/           # 論文庫（三層結構）
│   ├── README.md            # 第1層：所有已讀論文清單，每篇附重點概要與資料夾連結
│   └── <論文資料夾>/         # 第2層：每篇論文一個資料夾（從 _template 複製）
│       ├── paper.pdf        #   論文原始檔（收錄論文時一併複製進來）
│       ├── README.md        #   記錄該論文的每個重點 + 使用者對每個重點的理解程度
│       ├── supplements.md   # 第3層：論文中沒解釋、但使用者不懂的概念補充教學
│       └── slides/          #   這篇論文產出的投影片存放處
├── knowledge-map.md         # 跨論文概念總表：概念名稱｜理解程度｜出處（連結到具體論文）
├── goals.md                 # 長期計畫表，分「已完成」與「即將要做」兩區
├── plan-changelog.md        # 計畫調整紀錄：日期｜改變內容｜原因
├── dev-log/                 # 踩坑紀錄（memory）：日期／嘗試的方法／為何失敗／替代方案
├── weekly/                  # 週報存檔（PPT + MD）
├── profile/
│   ├── skills.md            # 使用者技能清單（含程度），持續更新
│   ├── interests.md         # 性向分析結果，持續更新
│   └── task-feelings.md     # 每次任務感受的原始紀錄
└── career-plan/
    ├── current-plan.md      # 目前的職涯整體規劃
    ├── changelog.md         # 職涯目標變更紀錄：日期｜變更內容｜原因
    └── job-targets.md       # 目標職缺與其 requirement
```

### skill 與 data 的對應關係

| Skill | 讀取 | 寫入 |
|---|---|---|
| research/1.qa-check-knowhow | paper-library/ | 論文資料夾 README.md、paper-library/README.md、knowledge-map.md |
| research/2.background-extension | 論文 README.md、knowledge-map.md | 論文 supplements.md |
| research/3.slide-maker | 論文 README.md、supplements.md | 論文 slides/ |
| research/4.review | 論文全部檔案 | 論文 README.md、knowledge-map.md |
| develop/goal-planner | profile/skills.md | goals.md |
| develop/plan-adjuster | goals.md | goals.md、plan-changelog.md |
| develop/dev-logger | dev-log/ | dev-log/ |
| develop/newtech-searching | goals.md | （回報給使用者，必要時寫入 dev-log/） |
| develop/weekly-report | goals.md、dev-log/ | weekly/ |
| career/story-builder | goals.md、dev-log/、plan-changelog.md、career-plan/changelog.md、profile/task-feelings.md | （產出面試故事素材） |
| career/leetcode-training | dev-log/、開發程式碼 | （問答驗證） |
| career/job-matching | profile/skills.md、career-plan/ | profile/skills.md、career-plan/changelog.md、career-plan/current-plan.md |
| career/interest-tracker | profile/task-feelings.md | profile/task-feelings.md、profile/interests.md |

## 3. 收到新論文時的處理流程

使用者丟一篇新論文（PDF／連結／文字）時，依序執行下列四個 skill。每一步的產出都是下一步的輸入，所以**預設不跳步**——但使用者可以指定從任一步開始或喊停。

| 步驟 | Skill | 開工前必做的檢查 | 產出 |
|---|---|---|---|
| 1 | `research/1.qa-check-knowhow` | **先問使用者與本篇的接觸程度**（沒接觸過／接觸過未讀本篇／掃過細節不熟／完全讀過），據此調整出題深度與起點 | 論文資料夾（含 `paper.pdf`）、該論文 README 的重點清單與理解程度、第1層總表、knowledge-map |
| 2 | `research/2.background-extension` | 讀該論文 README 找出「不懂／略懂」的概念 | `supplements.md`（A 區＝論文沒解釋的背景知識；B 區＝論文有講但需重講的重點） |
| 3 | `research/3.slide-maker` | **先產出大綱＋風格選項給使用者確認**，確認後才動工 | `slides/` 底下的 pptx 與 pdf、骨架版與完整版講稿與音檔 |
| 4 | `research/4.review` | **若非首次複習，先從待複習清單抽考** | 四階段（懂／會／記／說）結果、待複習清單更新、理解程度升降 |

**彈性規則**：
- 使用者已熟悉的論文可直接從步驟 3 或 4 開始。
- 步驟 4 可反覆執行（間隔重複），每次都先抽考清單。
- 每完成一個步驟，都要跑第 4 節「每次工作結束的固定流程」。
- 使用者中途提出流程改進時，**當下就寫回對應的 SKILL.md**，不要只在對話裡答應。

## 4. 每次工作結束的固定流程

每次完成一項工作（任何 skill 或任務）後，**主動詢問使用者**：

1. 是否要執行 `dev-logger`？（本次是否有踩坑、發現不可行的方法值得記錄？）
2. 是否要執行 `interest-tracker`？（記錄本次任務的感受：喜歡／不喜歡＋原因）
3. **skill 通用性檢查**（本次有執行或修改過 skill 時才需要）——由 agent 主動做，再把結果報給使用者：
   - **這次新增／修改的規則，是通則還是這次任務的特例？** 邊做邊改 skill 很容易把特例寫成通則。特例要改寫成「通則＋舉例」，或至少標注「例：」。
   - **有沒有哪條既有規則這次套不上去、或得違反才能完成任務？** 那條就是不夠通用，要修。
   - **快速掃法**：`grep` skill 檔案裡的專有名詞（論文名、工具名、專案名、數字），確認每一個都是舉例而非規則本體；寫死的數字改成比例或原則。
   - 也要反向檢查：規則有沒有隱含假設某種論文類型／作業系統／檔案格式，換一種就會失效。

## 5. 語言規則

**回答一律使用繁體中文。**
