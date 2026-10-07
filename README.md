# verify-content v2.0

**多媒體內容查證 Skill**

`verify-content` 是一套面向 ChatGPT / Codex / Claude Code 等 Agent 工作流的事實查核規格，支援文字、網址、圖片、影片、音訊、PDF、Office 文件、Spreadsheet 與科學研究內容。

## 核心特色
- Atomic Claim Extraction
- 原始／官方來源優先
- Source Quality + Source Independence
- Citation Support Validation
- Counter-evidence Search
- Recency / Numerical / Causality / Extrapolation Check
- 九類 Verdict Labels
- High / Medium / Low Confidence
- Image / Video / Audio / Document Verification
- Scientific / Medical / Educational Verification
- Safe-to-share 修正版

## Repository

```text
verify-content/
├── SKILL.md
├── README.md
├── CHANGELOG.md
├── VERSION
├── LICENSE
├── references/
│   ├── source-quality.md
│   ├── verification-rubric.md
│   ├── scientific-evidence.md
│   ├── media-verification.md
│   ├── medical-safety.md
│   ├── output-template.md
│   └── workflow.md
└── examples/
    ├── text-fact-check.md
    ├── image-fact-check.md
    ├── science-claim.md
    ├── social-post.md
    └── teaching-content.md
```

## 快速使用
對 Agent 說：

```text
查證
```

並附上文章、網址、圖片、影片或文件。

也可以指定：

```text
用 verify-content Deep 模式查證這篇文章。
```

## 核心哲學
> 查證的核心不是搜尋，而是控制推論。

Evidence → Interpretation → Inference → Conclusion

## License
MIT
