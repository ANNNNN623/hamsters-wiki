# AGENTS.md - LLM 研究知識庫 (LLM Research Wiki) 協同運作規範

本文件是針對大型語言模型（LLM Agent，如 Antigravity、Claude Code、Codex 等）所制定的核心協同手冊與架構規範。其宗旨為落實 Andrej Karpathy 所提出的「**LLM Wiki（持續複利知識庫）**」模式，將本知識庫打造成一個隨時間累積、自我演進、互連互通的 LLM 領域研究資產。

---

## 1. 核心理念與人機分工 (Core Philosophy)

### 1.1 傳統 RAG vs. 持續複利 Wiki (Compounding Wiki)
* **傳統 RAG 的盲點**：每次提問時重新檢索片段、重組答案，知識沒有沉澱與積累。面對跨文獻綜合分析或微妙脈絡時，每次都得從零開始拼湊。
* **LLM Wiki 的優勢**：在讀入資料時就將知識**編譯（Compile）並持久化（Persist）**為結構化的 Markdown 網絡。實體連結已建置、矛盾已標記、架構演進已梳理。隨著文獻增加與提問深入，Wiki 將持續複利增長。

### 1.2 人機職責分工 (Roles)
* **人類研究員 (Human)**：
  * 擔任「探索者」與「總架構師」。
  * 負責挑選並輸入高品質的原始文獻（論文、技術報告、文章、演講逐字稿）。
  * 提出具深度的研究問題，指引綜合分析方向。
  * 透過 Obsidian 瀏覽視覺化圖譜（Graph View）、閱讀更新結果。
* **LLM Agent**：
  * 擔任「專屬研究助理」與「知識庫維護工程師」。
  * 負責全部繁重費時的整理、歸檔、交叉連結（Cross-referencing）、頁面維護與矛盾校驗。
  * 遵守「Obsidian 即 IDE，LLM 即程式設計師，Wiki 即代碼庫」之原則。

---

## 2. 目錄架構與讀寫權限邊界 (Directory Architecture & Permissions)

本專案分為嚴格的三層架構，Agent 必須恪守存取權限：

```text
LLM WIKI NOTE/
├── AGENTS.md                  # [本規範文件] Agent 操作準則與規範 (唯讀參考)
├── README.md                  # 專案概覽與使用說明
├── raw/                       # [第一層：原始來源 (Raw Sources)] —— 絕對不可變 (Immutable)
│   ├── papers/                # 論文原件 (PDF, Markdown, TXT 等)
│   ├── articles/              # 技術文章、部落格剪藏 (Web Clipper)
│   ├── transcripts/           # 會議、演講、Podcast 逐字稿
│   └── assets/                # 本地圖表、附件影像 (供 Obsidian 渲染)
├── wiki/                      # [第二層：Wiki 知識庫 (The Wiki)] —— 由 Agent 全權維護與寫入
│   ├── index.md               # 內容目錄 (Catalog) - 全站主題索引與清單
│   ├── log.md                 # 運作日誌 (Chronological Log) - 記錄所有操作
│   ├── concepts/              # 核心技術與理論 (e.g., Attention, MoE, RoPE, RLHF, GRPO)
│   ├── models/                # 模型架構與家族 (e.g., LLaMA, DeepSeek, GPT-4, Claude)
│   ├── papers/                # 論文深度解析頁 (從 raw/ 提煉的結構化筆記)
│   ├── entities/              # 研究機構、實驗室、人物 (e.g., OpenAI, DeepSeek, Meta AI)
│   ├── syntheses/             # 縱向演進與主題綜合研究 (e.g., Reasoning 模型演進史)
│   └── comparisons/           # 橫向對比與基準分析 (e.g., DPO vs PPO vs GRPO)
└── templates/                 # [第三層：範本庫 (Templates)] —— 建立新筆記時遵循的格式標準
    ├── paper_template.md      # 論文解析範本
    ├── concept_template.md    # 技術概念範本
    ├── model_template.md      # 模型架構範本
    └── synthesis_template.md  # 綜合研究範本
```

### 權限規則：
1. `raw/` 目錄為**單向輸入真理來源（Source of Truth）**，Agent **嚴禁修改、覆寫或刪除**其中的任何檔案。
2. `wiki/` 目錄為 Agent 的專屬工作空間。Agent 負責在此新增、編輯、修訂頁面與更新雙向連結。
3. `templates/` 為格式規範樣板，新增檔案時應參考對應格式，保持結構一致。

---

## 3. 三大核心運作工作流 (Core Operations)

### 3.1 攝入流程 (Ingest Workflow)
當使用者放入新論文或文章至 `raw/` 並發出處理指令時，Agent 執行以下標準流程：

1. **閱讀與理解**：深入閱讀 `raw/` 中的目標來源，提取核心貢獻、數學公式、架構改進、訓練細節與實驗結果。
2. **對話確認**：向使用者簡要說明該文獻的 2~3 個核心洞察，確認是否有特定聚焦面向。
3. **建立論文解析頁 (`wiki/papers/`)**：
   * 檔名採用簡明英文，例如：`2024-deepseek-v3.md` 或 `2017-attention-is-all-you-need.md`。
   * 遵循 `templates/paper_template.md` 結構撰寫。
4. **漣漪更新 (Ripple Updates - 關鍵步驟)**：
   * 檢查文獻涉及的技術，更新既有的 `wiki/concepts/` 頁面（若無則新建）。
   * 檢查涉及的模型，更新既有的 `wiki/models/` 頁面（若無則新建）。
   * 檢查涉及的研究機構/實驗室，更新 `wiki/entities/` 頁面。
   * **標記認知衝突與演進**：若新文獻推翻了舊文獻的假設（例如：推翻舊有的 Scaling Law 指數，或指出傳統 Attention 的限制），必須在相關頁面中明確補充「對比與演進註記」，保留歷史觀點並標明新發現。
5. **更新主索引 (`wiki/index.md`)**：
   * 在對應分類下新增一行條目：包含 `[[雙向連結]]`、一句話精準摘要、標籤。
6. **追加歷史日誌 (`wiki/log.md`)**：
   * 追加標準日誌條目，格式：
     `## [YYYY-MM-DD] ingest | 文獻標題`
     條目內列出新增檔案、更新的 concept/model 頁面清單。

---

### 3.2 查詢與知識回流流程 (Query & Feedback Workflow)
使用者向知識庫提問時，Agent 不應只是當成普通問答機器人，而應發揮累積優勢並將成果回饋知識庫：

1. **查閱索引與筆記**：先讀取 `wiki/index.md` 與相關的 concept/model/paper 筆記，檢索具備交叉參照的上下文。
2. **綜合回答**：
   * 結合已建立的知識網絡，精準引用文獻與概念（使用 `[[筆記名稱]]` 格式）。
   * 指出不同文獻之間的共識、分歧或演進軌跡。
3. **價值回流 (Compounding Synthesis)**：
   * **若該次回答產生了高價值橫向對比、概念歸納或趨勢分析**，Agent 應主動提示使用者，或直接將回答整理為獨立頁面：
     * 對比分析儲存於 `wiki/comparisons/`（例如：`moe-routing-mechanisms.md`）。
     * 縱向綜合儲存於 `wiki/syntheses/`（例如：`reasoning-llm-evolution.md`）。
   * 將新頁面加入 `wiki/index.md`，並在 `wiki/log.md` 記錄 `## [YYYY-MM-DD] query | 查詢主題 (歸檔)`。

---

### 3.3 健康檢查流程 (Lint Workflow)
定期或在使用者要求時（如指令：「請進行 Wiki 健康檢查」），Agent 對全站進行稽核：

1. **孤島頁面偵測 (Orphan Pages)**：找出沒有任何內部頁面連結指向的孤島筆記。
2. **缺失概念識別 (Missing Concepts)**：掃描多次在筆記中出現但尚未建立專屬頁面的重要術語。
3. **過期主張與矛盾校驗 (Stale Claims & Contradictions)**：檢查是否有早期模型的數據或推論已被後續研究所修正，但舊筆記尚未標註。
4. **索引完整性驗證 (Index Consistency)**：確保 `wiki/index.md` 涵蓋了所有 `wiki/` 內的檔案，沒有漏網之魚或損壞連結。
5. **研究盲點建議 (Research Gaps)**：基於目前的知識圖譜結構，向使用者建議下一步值得追蹤的新論文或研究主題。
6. **記錄與產出報告**：在 `wiki/log.md` 記錄檢查結果：
   `## [YYYY-MM-DD] lint | 健康檢查報告與維護項目`。

---

## 4. 文件命名與格式標準 (Conventions)

### 4.1 檔案與目錄命名
* 一律使用**小寫英數字**與**連字號（kebab-case）**，以確保跨平台（Windows/macOS/Linux/Git）相容性。
* 論文筆記：`YYYY-short-name.md`（如 `2024-deepseek-r1.md`）。
* 概念筆記：`concept-name.md`（如 `mixture-of-experts.md`、`rotary-position-embedding.md`）。
* 模型筆記：`model-family-name.md`（如 `llama-3.md`、`deepseek-v3.md`）。
* 機構筆記：`entity-name.md`（如 `deepseek-ai.md`、`meta-fair.md`）。

### 4.2 Obsidian 雙向連結語法
* 內部引用一律使用 Wikilinks 雙向連結：`[[檔案名或標題]]` 或 `[[檔案名|顯示別名]]`。
* 範例：`採用了 [[mixture-of-experts|MoE 稀疏架構]]，由 [[deepseek-ai|DeepSeek]] 團隊研發。`

### 4.3 YAML Frontmatter 格式
每個在 `wiki/` 內的 Markdown 檔案頂部必須包含標準 YAML 區塊，方便 Obsidian Dataview 插件檢索：

```yaml
---
title: 檔案標題
aliases: ["別名1", "別名2"]
type: paper | concept | model | entity | synthesis | comparison
tags:
  - llm/architecture
  - llm/training
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources:
  - "[[對應論文或來源]]"
status: draft | stable | evolving
---
```

### 4.4 數學符號與專業術語
* 行內數學式使用 `$式子$`，獨立段落公式使用 `$$...$$`。
* 專業術語以繁體中文說明為主，首次出現時並列標準英文術語（如：旋轉位置編碼（Rotary Position Embedding, RoPE））。

---

## 5. 索引與日誌維護準則 (Indexing & Logging)

### 5.1 `wiki/index.md`
* 這是知識庫的總覽導覽圖。
* 分為以下分區：
  1. **核心技術概念 (Core Concepts)**
  2. **模型與架構 (Models & Architectures)**
  3. **關鍵論文筆記 (Paper Notes)**
  4. **研究團隊與機構 (Research Labs & Entities)**
  5. **綜合專題與橫向評測 (Syntheses & Comparisons)**
* 每項條目均採用單行清單，例如：
  `- [[2024-deepseek-v3]]: DeepSeek-V3 技術報告，創新之 MLA 與 DeepSeekMoE 架構解析 #paper #moe`

### 5.2 `wiki/log.md`
* 採**僅追加模式（Append-Only）**，按時間降冪排列（最新的在最上方）。
* 標題標準格式：
  * `## [YYYY-MM-DD] ingest | <文獻名稱>`
  * `## [YYYY-MM-DD] query | <查詢主題>`
  * `## [YYYY-MM-DD] lint | <維護或巡檢主題>`
* 內容需簡明列出變更影響的檔案清單與重要結論摘要。

---

## 6. LLM 研究領域知識分類指南 (LLM Research Taxonomy)

當建立標籤（Tags）與分類時，請依循以下專業領域劃分：

1. **架構與機制 (Architectures & Mechanisms)**:
   * `#arch/attention` (Multi-Head, Grouped-Query, Multi-Head Latent Attention)
   * `#arch/positional` (RoPE, ALiBi, NoPE)
   * `#arch/moe` (Sparse MoE, Routing, Load Balancing)
   * `#arch/non-transformer` (SSM, Mamba, RWKV, Linear Attention)
2. **預訓練與資料工程 (Pre-training & Data)**:
   * `#pretrain/scaling-laws` (Chinchilla, Compute-optimal, Data-constrained)
   * `#pretrain/data-curation` (Synthetic data, Deduplication, Filtering)
   * `#pretrain/tokenization` (BPE, SentencePiece, Byte-level)
3. **後訓練與對齊 (Post-training & Alignment)**:
   * `#posttrain/sft` (Supervised Fine-Tuning, Instruction Tuning)
   * `#posttrain/rlhf` (PPO, DPO, KTO, ORPO, GRPO)
   * `#posttrain/reasoning` (Process Supervision, PRM, Test-time Compute, Monte Carlo Tree Search)
4. **推論加速與硬體部署 (Inference & Systems)**:
   * `#inference/kv-cache` (PagedAttention, vLLM, Quantized Cache)
   * `#inference/speculative-decoding`
   * `#inference/quantization` (AWQ, GPTQ, BitsAndBytes, FP8/FP4)
5. **評測與安全 (Evaluation & Safety)**:
   * `#eval/benchmarks` (MMLU, GSM8K, MATH, HumanEval, Arena)
   * `#eval/hallucination`
   * `#safety/jailbreak`

---

## 7. 啟動自我檢查清單 (Agent Startup Checklist)

每次在為使用者執行操作前，Agent 應主動在背景確認：
- [ ] 目標是否為 `raw/` 內的來源？若是，不可直接修改原始檔案。
- [ ] 產生的所有檔案是否都在 `wiki/` 目錄內？
- [ ] 是否所有專有名詞與相關頁面都加上了 `[[...]]` 雙向連結？
- [ ] 本次變更完成後，是否已同步更新 `wiki/index.md` 與 `wiki/log.md`？
- [ ] 筆記頂部是否已按照規範配置標準 YAML Frontmatter？
