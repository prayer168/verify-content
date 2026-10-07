# verify-content

> 中文名稱：多媒體內容查證  
> Version: 2.0.0  
> Category: Verification / Fact-checking / Research  
> Default language: Traditional Chinese (zh-TW)

## Purpose

`verify-content` 是一套通用型多媒體事實查核 Skill。它不是單純搜尋資料，而是把輸入內容拆成可驗證主張，追溯原始證據，檢查來源是否真的支持主張，搜尋反證與限制，最後給出分級判定與可安全引用的修正版。

核心原則：

> 查證的核心不是「找到來源」，而是「確認證據真正支持到什麼程度」。

> Evidence first. 沒有足夠證據，就降低結論強度，不以推測補滿缺口。

## Trigger

以下情況自動啟用：

- 查證、幫我查證、事實查核、Fact Check
- 這是真的嗎？真的假的？
- 這篇文章正確嗎？這個說法有根據嗎？
- 幫我確認來源／核實／找原始研究
- 這張圖是真的嗎？這影片是真的嗎？
- 這是不是 AI 生成？
- 這研究是真的嗎？幫我確認數據
- 這個新聞可信嗎？這個說法有沒有誇大？
- 這篇可以轉貼嗎？可以拿來教學生嗎？

若使用者只說「查證」，但同一則訊息附有文字、網址、圖片、影音或文件，也自動啟用。

## Supported inputs

- 純文字、文章、新聞、社群貼文
- URL
- 圖片、截圖、圖表、Infographic
- YouTube／影片／音訊／Podcast
- PDF、Word、PowerPoint、Markdown
- Excel／Spreadsheet
- 科學文章、教材、AI 生成內容
- 多媒體混合輸入

## Modes

### Quick
適合單一說法、短貼文、單張圖片。擷取 1–5 個關鍵主張，快速查核。

### Standard
預設模式：
1. 理解內容
2. 拆解原子化主張
3. 搜尋原始與官方證據
4. 來源分級
5. 檢查來源獨立性
6. 搜尋支持與反證
7. 驗證引用是否真正支持主張
8. 逐項判定
9. 整體可信度
10. 修正版

### Deep
適合科學、醫療、教育研究、環境、公共政策與爭議性議題。增加原始論文、DOI、方法、樣本、統計、系統性回顧、反方文獻與 Evidence Gap 分析。

## Atomic claim extraction

禁止把整篇內容只判定為「真／假」。應拆成原子化主張。

例：

> 薰衣草精油可以殺死空氣中的細菌，因此用擴香器可以預防感冒。

拆解為：
1. 薰衣草精油具有抑菌效果。
2. 研究證實可抑制空氣中的細菌。
3. 家用擴香器可產生相同效果。
4. 此效果能降低人體感冒風險。

四項必須分別查證，不能因第 1 項成立就推定第 2–4 項成立。

## Claim types
- Factual Claim
- Numerical Claim
- Causal Claim
- Scientific Claim
- Forecast Claim
- Historical Claim
- Medical / Health Claim

對因果主張要特別防止「相關性 → 因果」錯誤。

## Source hierarchy

### Level S — Primary / Official
原始研究、政府、官方統計、法規、官方技術文件、原始資料集、國際組織原始報告。

### Level A — Authoritative
大學、研究機構、專業學會、系統性回顧、Meta-analysis、教科書級資料。

### Level B — High-quality Secondary
高品質科學媒體、主流媒體、專業媒體。應盡量回溯原始來源。

### Level C — General Websites
一般網站、部落格、商業網站。只作輔助證據。

### Level D — Social Media
Facebook、Threads、X、YouTube、TikTok、LINE 轉傳。不得單獨證明重要事實。

## Evidence quantity
一般重要主張：優先至少 2 個彼此獨立的可信來源。  
重大、高風險或爭議性主張：優先至少 3 個獨立來源。  
來源數量不能取代品質；多篇互抄的新聞只算一個資訊來源。

## Primary-source rule

只要二手資料寫「一項研究發現……」，應盡量找到原始研究，核對：
- Title
- Authors
- Journal
- Year
- DOI
- Population
- Sample size
- Method
- Results
- Limitations

## Mandatory validator layer

每一個重要主張必須通過：
1. Source quality
2. Source independence
3. Citation support
4. Counter-evidence
5. Recency
6. Numerical validation
7. Causality validation
8. Extrapolation validation
9. Certainty calibration

詳細規則見 `references/`。

## Verdict labels

- ✅ 正確：核心內容與可靠證據一致。
- 🟢 大致正確：核心成立，但有少量簡化或細節誤差。
- 🟡 部分正確：部分成立，但另有重要錯誤或未證實內容。
- 🟠 缺乏脈絡：句子未必錯，但缺少必要條件、時間、範圍或背景。
- ⚠️ 誇大或誤導：有事實基礎，但結論超出證據。
- 🔴 錯誤：與可靠證據明顯矛盾。
- ❓ 尚無法證實：目前沒有足夠可靠證據支持或否定。
- 🕒 已過時：過去可能成立，但已有更新資訊取代。
- 💬 非事實主張：價值判斷、意見、修辭、信仰等，不宜硬判真假。

## Confidence

每項主張附信心等級：
- High：官方／原始證據充分，多來源一致，沒有重大矛盾。
- Medium：有合理證據，但資料有限或存在不確定性。
- Low：來源少、原始資料難取得、證據衝突或高度依賴推論。

## Default output

# 查證結論

**整體判定：［標籤］**

用 2–5 句說明：
- 哪些內容可信
- 哪些需要修正
- 最大風險在哪裡

## 逐項查證

| # | 原始主張 | 判定 | 查證結果與必要脈絡 | 核心證據 | 信心 |
|---|---|---|---|---|---|

必要時增加：
- 最關鍵的誤導
- 建議修正版
- 可安全轉貼版本
- 臺灣來源／國際或原始來源

## Media rules

### Image
分三層：
1. 圖中文字與數字
2. 圖像內容與場景是否符合宣稱
3. Provenance：原始發布者、日期、圖說、官方版本

### Video
拆成：影片本身 → 可驗證主張 → 來源 → 時間 → 畫面與說法是否一致。  
若無法取得影片，不得假裝已觀看。

### Audio
先取得可用內容或逐字稿，再拆主張與查證。不得因說話者自稱某身分就視為已確認。

### Documents
PDF、Word、PowerPoint、Spreadsheet 應先掌握文件結構，再擷取重要主張、數據、圖表、引用與結論，避免只查摘要或第一頁。

## Scientific rules

禁止下列直接外推：
- in vitro → humans
- animal study → humans
- one experiment → scientific consensus
- association → causation
- simulation → proof of real-world mechanism
- short-term result → long-term effect
- limited sample → universal conclusion

## Educational-content rules

自然科與教材查證同時評估：
1. 科學概念是否正確？
2. 教學實驗是否真的能證明該概念？

應指出實驗能證明什麼、不能證明什麼、哪些變項未控制。

## Historical / cultural rules

必須區分：
- 史料可證實
- 傳統說法
- 民間傳說
- 後世附會

「流傳很廣」不能等同「史實」。

## Date normalization

遇到今天、昨天、最近、今年等相對日期，盡可能轉換成 YYYY-MM-DD，並核對真正事件或發布日期。

## Numerical validation

數據型主張至少確認：
- number
- unit
- denominator
- sample size
- time range
- geographic scope
- measurement method

## Research validation

研究型內容至少核對：
- 論文是否存在
- DOI 是否正確
- 作者、年份、期刊
- 研究方法
- 樣本
- 對照組
- 結果
- 限制

禁止虛構 DOI、論文、作者、官方文件或統計。

## AI-generated-content detection

不能僅憑手指、字體、光影或「畫面怪異」就斷言 AI 生成。

應區分：
- 可疑視覺特徵
- 來源證據
- metadata
- 原始發布資訊
- 最終信心

沒有可靠來源證據時，使用「可能為 AI 生成」，不要說「一定」。

## Self-validation loop

輸出前再檢查：
- Source Check
- Support Check
- Date Check
- Number Check
- Causality Check
- Extrapolation Check
- Counter-evidence Check
- Certainty Check

任一項失敗時，降低判定或信心水準。

## Failure handling

遇到來源不存在、網頁失效、影片不可讀、論文受限、圖片來源不明、證據衝突時：
- 不自行補內容
- 清楚說明「目前無法確認」
- 說明已確認到哪裡
- 說明還缺少什麼
- 不把搜尋摘要當作原始內容

## Core philosophy

> 查證的核心不是搜尋，而是控制推論。

一篇內容即使引用、論文、數字都是真的，最終結論仍可能錯。必須檢查：

Evidence → Interpretation → Inference → Conclusion

真正的 Fact Check 不只問：
「來源是真的假的？」

還要問：
「證據真的足以推出這個結論嗎？」
