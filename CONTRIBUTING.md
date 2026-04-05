# Contributing to Prism

## Ways to Contribute

### 1. Create Your Own Prism Instance

The most valuable contribution is showing that the framework works for different people. Fork the repo, build your own, and share it.

**Steps:**

1. Fork this repo
2. Copy `ask-eric/` to `ask-yourname/` (the plugin's `"skills": "."` in `plugin.json` auto-discovers all skill directories at the repo root)
3. Edit `SKILL.md`:
   - Update the `name` and `description` in frontmatter
   - Rewrite the persona section with your own identity and voice
   - Adjust the dispatch matrix if your priorities differ
   - Write your own anti-patterns (what does generic advice look like in your domain?)
4. Edit each file in `perspectives/`:
   - Keep the structure (core principles, judgment criteria, anti-patterns, output format)
   - Replace the content with your own principles and examples
   - Not every perspective needs to be deep — focus on the ones that represent your strongest opinions
5. Create your universal doc (`yourname-engineering-mind.md`)
6. Test with real questions and iterate

**You don't need all 20 perspectives.** Start with the 5-7 that matter most to you. A focused Prism with 7 deep perspectives is better than 20 shallow ones.

### 2. Improve Existing Perspectives

If you have domain expertise that could strengthen a perspective:

- Add concrete anti-patterns (the "don't do this / do this" tables)
- Add judgment criteria that are missing
- Improve the examples to be more specific and less generic
- Fix inaccuracies

### 3. Propose New Perspectives

If you think there's a missing perspective:

1. Open an issue using the "New Perspective Proposal" template
2. Describe:
   - What question does this perspective answer?
   - Which layer does it belong to?
   - Why can't existing perspectives cover this?
   - Give 2-3 example situations where this perspective would change the output

### 4. Report Issues

- Skill produces generic advice instead of distinctive output? File a bug.
- Perspective advice is wrong or outdated? File a bug.
- Dispatch logic picks wrong perspectives? File a bug with the input and expected behavior.

## Writing Guidelines

### Perspective Files

Every perspective file should have:

```markdown
# [Name] Perspective

[One sentence: what voice does this perspective represent?]

## Core Principles
[3-5 principles, each with a concrete explanation, not abstract]

## Anti-Patterns
[Table: "Don't do this" vs "Do this" with specific examples]

## Judgment Criteria
[5 questions to ask when analyzing from this perspective]

## Output Format
[What the perspective's analysis should look like]
```

### Voice

- **Be opinionated.** "I prefer X because Y" is better than "consider X or Y"
- **Be concrete.** Show the SQL injection payload, don't just say "watch out for injection"
- **Be honest.** If something is a trade-off, say what you're giving up
- **Use anti-patterns.** Every perspective should know what "generic AI advice" looks like and avoid it

### Language

- The `ask-eric` instance is in Traditional Chinese. Your instance can be in any language.
- Framework-level docs (this file, root README) are in English for accessibility.
- Keep perspective files in whatever language your target users speak.

## Pull Request Process

1. Fork and create a branch from `main`
2. Make your changes
3. Test by running real questions through the skill (describe what you tested in the PR)
4. Submit PR using the template
5. Maintainer reviews and merges

## Versioning

This project follows [Semantic Versioning (semver.org)](https://semver.org/)。版本號格式：`MAJOR.MINOR.PATCH`。

| 版本位 | 什麼時候升 | 範例 |
|--------|-----------|------|
| **MAJOR** | Breaking change — 使用者的 Prism instance 需要修改才能繼續使用（例：SKILL.md 格式變更、perspective 結構不相容、dispatch 機制重新設計） | 1.0.0 → 2.0.0 |
| **MINOR** | 新功能，向後兼容 — 新增視角、新增跨視角原則、擴充現有視角的重大段落、新增互動模式 | 1.0.0 → 1.1.0 |
| **PATCH** | 修正和改善 — 修 typo、修 stale reference、更新過時的標準（如 OWASP 版本）、統一格式、補反模式 | 1.1.0 → 1.1.1 |

**原則：**
- 版本號傳達的是「這次變更對使用者的影響程度」，不是「改了多少東西」
- 改了 100 個檔案但都是格式統一 → PATCH
- 只加了 1 個視角但改變了分析行為 → MINOR
- 如果不確定，偏向升高（PATCH vs MINOR 選 MINOR）— 寧可讓使用者多看 release note，不要讓他們漏掉重要變更
- 每次 release 都要更新 CHANGELOG.md 並建立 GitHub Release

## Code of Conduct

Be constructive. The whole point of Prism is multi-perspective thinking — disagreement is expected and valuable when it's about ideas, not people.
