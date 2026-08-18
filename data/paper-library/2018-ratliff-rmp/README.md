# Riemannian Motion Policies

## 基本資訊

- **作者**：Nathan D. Ratliff, Jan Issac, Daniel Kappler, Stan Birchfield, Dieter Fox（NVIDIA / Max Planck）
- **發表處／年份**：arXiv:1801.02854v3, 2018
- **連結**：https://arxiv.org/abs/1801.02854
- **官方 demo 影片**：[Research at NVIDIA: RMPflow – A Computational Graph for Automatic Motion Policy Generation](https://www.youtube.com/watch?v=Fl4WvsXQDzo)
- **一句話摘要**：提出 RMP——把「加速度策略 + Riemannian 度量」綁成一個數學物件，讓多個運動策略能在不同 task space 間做幾何一致的轉換與合成，證明其最優性，統一了 operational space control、DMP、MPC 等多種運動生成方法。

## 重點清單與理解程度

理解程度等級：`不懂`／`略懂`／`懂`／`精通`

| # | 重點 | 說明 | 理解程度 | 備註 |
|---|---|---|---|---|
| 1 | 動機：局部反應式策略的合成問題 | 全域規劃太慢、局部反應快但多個策略疊加（naive superposition／pseudoinverse）會互相打架、震盪（例：兩側障礙物斥力對稱抵銷後被忽略）。RMP 要解的就是「多策略如何正確合成」 | 略懂 | 未直接測，Q1 回饋中有講解 |
| 2 | RMP 定義：(f, A) | f 是二階動力系統（位置+速度 → 期望加速度，即 acceleration policy）；A(x, ẋ) 是隨狀態平滑變化的半正定 Riemannian 度量，編碼「這個策略在意哪些方向」 | 懂 | Q1 誤解 A 為「阻力」；經 supplements 概念1 教學後，2026-08-15 檢驗通過（發言權語言正確解釋方向性設計與打架機制） |
| 3 | 三大運算子：addition / pullback / pushforward | addition = metric 加權平均（式 8–9）；pullback 把 task space 的 RMP 拉回 C-space：(J⁺f, JᵀAJ)（式 10–11）；pushforward 反向。具線性、結合律、座標協變性 | 懂 | Q2 誤以為 Jᵀ 有「反矩陣的感覺」；經教學後理解「先換算再打分」，並自行確認 pullback 方向（任務→關節、f 與 A 一起搬） |
| 4 | 與 natural gradient 的類比 | pullback metric JᵀAJ 對應機器學習中 natural gradient 的協變轉換；RMP 可視為 natural vector field | 不懂 | 未測；需要 ML 的 natural gradient 背景，論文未解釋 → background-extension 候選 |
| 5 | C-space 合成的最優性 | 合成解 = arg min Σ ½‖ẍᵢᵈ − Jᵢq̈‖²_{Aᵢ}（式 21），每個 RMP 是一個二次項（f 是最小值點、A 是 Hessian，類比 Gaussian 的 mean/variance）；結果與集中式 QP 等價但保有模組化 | 懂 | 隨概念1 檢驗通過一併鞏固（加權平均→分方向發言權→合成） |
| 6 | 基本局部策略庫 | target attractor（soft-normalization s(v)，式 23–24）、orientation（對軸上 canonical point 放 attractor）、collision（斥力+方向性阻尼，A=w·s ssᵀ，式 25–26）、redundancy resolution（C-space spring-damper 拉回預設姿勢） | 懂 | Q3 soft-normalization 曾答反；經 supplements 概念4（公式逐字拆解）教學後，2026-08-15 檢驗通過（α/β 失調行為、f 與 A 分工均正確） |
| 7 | Directionally stretched metric | A_stretch = ξξᵀ 只在意單一方向；常用 pattern：β·A_stretch+(1−β)I 再乘權重 w(x)（式 58–60）。度量的 eigenspectrum 定義策略在意的方向，是 soft nullspace | 懂 | 2026-08-15 檢驗通過：能解釋垂直方向設 0 的理由與設高的後果 |
| 8 | 整合慢速優化器（MPC/RieMO） | 計算昂貴的 MPC 在慢迴圈（10–20 Hz）把最優解線性化成 linear RMP（π* + ∇²Q，式 92）串流給快的 RMP core（1 kHz）合成 | 略懂 | Q5-1：慢引導快、失敗重規劃的架構對，但誤以為送的是切塊路徑目標點；實際送的是線性化策略＋度量 |
| 9 | 長程導航啟發式 | retract heuristic（先縮回 canonical 姿勢再伸出，倒放縮回=伸出）＋ guiding points（粗略 IK 引導），手肘不被擋就不需完整規劃器 | 懂 | Q5-2：安全返回點概念正確 |
| 10 | Joint limit 處理 | 用 sigmoid 映射把受限 C-space 對應到無約束空間：值域有界保證絕不越界；σ′ 在極限附近趨零使 Jacobian 對應行降權（式 72–83），且只壓制「朝極限移動」的方向 | 懂 | Q4：σ′ 漸小機制答對；補充了值域保證與速度方向 gating。對應 RMPflow 的 joint_limit_buffers |
| 11 | 實驗結論 | metric 換成 uninformative（βI）後控制器互相打架、性能大幅退化甚至撞障礙；150 個控制器搶 7 DOF 仍穩定；同組控制器跨機器人幾乎免調參 | 略懂 | 未直接測，總覽中有說明 |

**Q&A 施測日期**：2026-08-14（5 題）。總評：實作經驗帶來的直覺不錯（阻尼、joint limit、retract），但數學核心（A 的合成角色、JᵀAJ 的意義）普遍是「會用但說不清」，是 background-extension 與複習的重點。

## 與自身專案的關聯

- Isaac Sim 的 Lula/RMPflow 就是此框架的實作；G1 reach demo 手刻的 `g1_rmpflow_common.yaml` 調參（joint_limit_buffers、body_cylinders）都對應本論文概念（重點 6、10）。

## 待複習清單（間隔重複用，由 review skill 維護）

規則：答錯／答不出／答得含糊就入列並累計次數；下次 review 先從這裡抽考，通過才移出。**次數 ≥ 2 的是頑固誤解，優先處理。**

| # | 項目 | 錯誤次數 | 錯在哪裡 | 正確版本 | 狀態 |
|---|---|---|---|---|---|
| 1 | 慢迴圈傳給快迴圈的內容 | **2** ⚠️ | 說成「傳線性化的目標點」 | 傳的是 linear RMP＝線性化策略＋它的度量；格式與其他 RMP 相同才能一起加權合成 | 2026-08-17 回考通過（答出「少了度量會退化成各方向一樣」），但初答仍錯，保留觀察 |
| 2 | Target attractor 為何不爆炸 | **2** ⚠️ | 說成「距離 × 加速度倍數」（那是彈簧，反而會爆炸） | 靠 s(·) 柔性正規化：遠處把誤差長度壓掉只留方向，拉力飽和成定值 α；近處平滑歸零 | 待回考 |
| 3 | f／A／J 的標籤 | **3** ⚠️ | f 說成「目標點」、A 說成「加速度」、A 說成「Jacobian 權重矩陣」 | f＝加速度策略（想要什麼）、A＝黎曼度量（哪些方向多在意）、J＝Jacobian（關節動→末端動多少的換算表） | 待回考 |
| 4 | 式 21 的結構 | 1 | 與式 23（attractor）混淆 | 對 q̈ 最小化：Σ「策略想要的加速度 − 實際會得到的加速度」²，用各自的 Aᵢ 加權 → 眾人不滿意度的加權總和最小 | 待回考 |
| 5 | 避障度量的形狀 | 1 | 答「球形」（與 Isaac Sim 的 collision sphere 混淆）——球形＝單位矩陣，正是論文的反例對照組 | A = w(d)·ŝŝᵀ，ŝ 為指向障礙物的單位向量；ŝŝᵀ 是「一根針」，只在該方向有值 | 2026-08-17 回考通過（能推出球形會導致貼著走也被煞車） |
| 6 | sigmoid 的「絕不越界」保證 | 1 | 只答出函數名，未答出關鍵特性 | 來自**值域有界**（輸出恆在上下限內）；斜率趨零是「怎麼慢下來」，不是「為何不越界」 | 待回考 |
| 7 | directionally stretched metric 當設計工具 | 1 | G1 夾細長器械時方向設反（以為要在「往目標」方向高權重） | 度量要貼合任務的容錯方向：沿器械長軸棄權（哪裡夾都行）、垂直長軸高權重、手掌姿態最高（夾歪必敗） | 待回考 |
| 8 | MPC 慢迴圈頻率 | 1 | 記成 30 Hz | 每秒 10–20 次；快迴圈 100 Hz–1 kHz | 待回考 |
| 9 | α(d)、β(d) 的讀法 | 1 | 讀成「α 乘以 d」，因而以為越遠斥力越大 | 是**函數作用**：把距離餵進去。兩者隨距離遞減（附錄式 67 為指數衰減），越遠影響越小 | 待回考 |

**對照記憶**（第 2、9 項一起記）：目標吸引子「遠了不要更用力」（s 飽和成定值）；避障「遠了就別管」（α(d) 衰減到零）。

## 複習紀錄（由 review skill 更新）

| 日期 | 懂 | 會 | 記 | 說 | 弱點與下次重點 |
|---|---|---|---|---|---|
| | | | | | |
