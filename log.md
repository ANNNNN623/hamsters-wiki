# 知識庫演進日誌 (Wiki Activity Log)

本檔案為僅追加（Append-Only）的時間序日誌，記錄所有 Ingest、Query 歸檔與 Lint 維護操作。
每項條目皆以 `## [YYYY-MM-DD] <操作類型> | <說明標題>` 作為標頭，以利工具解析與檢索。

---

## [2026-11-16] query | 倉鼠照護規範與常見寵物鼠飼養指南（筆記與韓系簡報）
- **產出筆記**：`notes/2026-11-16-hamster-care-and-welfare.md`
- **產出簡報**：
  - 逐頁內容與講稿：`slides/2026-11-16-hamster-care/outline.md`、`content.md`
  - 互動式 HTML 簡報：`exports/2026-11-16-hamster-care.html`
- **檢驗邊界**：嚴格限定依據 Wiki 現存之台北市動保處指南、倉鼠/天竺鼠/絨鼠照護概念與對照表，標註國際福祉標準與獸醫醫療缺口。
- **文獻推薦**：文末整理 4 篇權威文獻與照護指南，附可一鍵直接下載 PDF 連結（Fischer 2007 籠具研究、英國 RVC 手冊、Oxbow 營養學手冊、洛杉磯 LA 照護指引）。

---

## [2026-11-16] query | 從 Attention 到現代 LLM 入門導讀與簡報製作
- **產出筆記**：`notes/2026-11-16-attention-and-transformer-foundations.md`
- **產出簡報**：
  - 逐頁內容與講稿：`slides/2026-11-16-attention-and-transformer/outline.md`、`content.md`
  - 互動式 HTML 簡報：`exports/2026-11-16-attention-and-transformer.html`
- **檢驗邊界**：嚴格限定依據 Wiki 現存之 Attention、Transformer、2017 論文與 Google Brain 知識，標註現代 LLM 知識缺口。
- **文獻推薦**：文末整理 4 篇可一鍵直接下載 PDF 之待入庫論文（RoPE, GQA, FlashAttention, LLaMA）。

---

## [2026-11-16] ingest | 臺北市鼠類飼養照護基本指南 (2023)
- **原始來源**：保存至 `raw/articles/2023-taipei-rodent-care-guide.md`
- **新建文獻筆記**：`wiki/papers/2023-taipei-rodent-care-guide.md`
- **漣漪更新 (Ripple Updates)**：
  - 新增概念頁面：
    - `wiki/concepts/hamster-care.md`（倉鼠飼養照護規範）
    - `wiki/concepts/guinea-pig-care.md`（天竺鼠飼養照護規範）
    - `wiki/concepts/chinchilla-care.md`（絨鼠飼養照護規範）
  - 新增機構實體：
    - `wiki/entities/taipei-animal-protection-office.md`（臺北市動物保護處）
  - 新增橫向對比：
    - `wiki/comparisons/rodent-care-comparison.md`（三物種生理與照護對照表）
- **索引更新**：已同步更新 `wiki/index.md`，納入相關概念、文獻、機構與對比頁面。
- **狀態**：完成攝入。

---

## [2026-11-16] init | 建立 LLM 研究知識庫與基礎規範
- **動作**：初始化 Wiki 專案架構與規範設定。
- **新增規範**：`AGENTS.md`、`README.md`。
- **建立目錄**：`raw/` (papers, articles, transcripts, assets), `wiki/` (concepts, models, papers, entities, syntheses, comparisons), `templates/`。
- **種子頁面**：
  - `wiki/concepts/attention-mechanism.md`
  - `wiki/concepts/transformer.md`
  - `wiki/papers/2017-attention-is-all-you-need.md`
  - `wiki/entities/google-brain.md`
- **狀態**：完成初始化，等待第一批論文/文章攝入。
