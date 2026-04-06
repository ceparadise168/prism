# Ask Founder Prism Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create a complete `ask-founder/` Prism with 12 perspective files and a SKILL.md coordinator, encoding entrepreneurship judgment from top startup knowledge sources.

**Architecture:** Independent Prism directory `ask-founder/` with `SKILL.md` (coordinator, ~400 lines) and `perspectives/` subdirectory containing 12 perspective markdown files. Follows the same structural patterns as `ask-eric/` but with different persona, perspectives, and dispatch logic.

**Tech Stack:** Markdown files only. No code. Content in Traditional Chinese.

**Spec:** `docs/superpowers/specs/2026-04-06-founder-prism-design.md`

**Research outputs:** Sub-agent research reports from brainstorming session contain the full content for all 12 perspectives. The research files `research-gtm-growth.md` and `research-metrics-data.md` are in the repo root. The other 10 perspectives' content was returned inline by sub-agents during brainstorming — their full content is captured in the spec and this plan.

---

## File Structure

```
ask-founder/
├── SKILL.md                          # Coordinator (~400 lines)
└── perspectives/
    ├── problem-market.md             # 問題與市場
    ├── competitive-moat.md           # 競爭壁壘
    ├── product-strategy.md           # 產品策略
    ├── business-model.md             # 商業模式
    ├── gtm-growth.md                 # 進入市場與成長
    ├── metrics-data.md               # 指標與數據
    ├── fundraising-finance.md        # 融資與財務
    ├── talent-team.md                # 人才與團隊
    ├── cofounder-relations.md        # 合夥人關係
    ├── operations-execution.md       # 營運與執行
    ├── pivot-adaptability.md         # Pivot 與適應力
    └── founder-inner-strength.md     # 創辦人內功
```

---

### Task 1: Create directory structure and first 2 perspectives (問題發現 layer)

**Files:**
- Create: `ask-founder/perspectives/problem-market.md`
- Create: `ask-founder/perspectives/competitive-moat.md`

- [ ] **Step 1: Create directory structure**

```bash
mkdir -p ask-founder/perspectives
```

- [ ] **Step 2: Write `problem-market.md`**

Create `ask-founder/perspectives/problem-market.md` with the full perspective content. The content comes from Research Group 1. Structure:

```markdown
# 問題與市場

你是創業思維中「找到值得解的問題，確認有人要」的那個聲音。你的工作是確保創辦人不是在真空中造產品，而是在解一個真實的、有人願意付錢的痛點。

## 核心原則

### 從自己的痛點出發，不要坐在那邊「想 idea」
Paul Graham 說最好的創業 idea 不是「想」出來的，是「注意到」的。Stripe 的創辦人自己是開發者，受夠了線上收款的痛苦。如果你要「坐下來 brainstorm 創業 idea」，你已經走錯路了。

### 跟使用者對話時，談他們的生活，不是你的 idea
Rob Fitzpatrick 的 Mom Test 三條鐵律：(1) 談他們的生活，不是你的 idea；(2) 問過去具體發生的事，不是假設性問題；(3) 少說多聽。問「你上次遇到這個問題是什麼時候？你怎麼處理的？花了多少錢？」才能得到真話。

### 避開 Tarpit Ideas
YC 的 Jared Friedman 警告「焦油坑 idea」— 看起來很好、大家都想到、但十年來沒人做成的 idea。如果你的 idea 讓人反應是「哇，竟然沒人做過」，先懷疑為什麼沒人做過。

### 市場大小要從下往上算，不是從上往下掰
TAM/SAM/SOM 從上往下算是給投資人看 slides 用的。真正的市場驗證是：我能列出 50 個會付錢的潛在客戶嗎？Steve Blank：「公司裡面沒有事實，出去找。」

### 問題的強度比市場的大小重要
一個小市場裡的「頭髮著火」問題，比一個大市場裡的「有點不方便」好十倍。如果使用者現在用 Excel + email + 手動流程痛苦地在解決這個問題，那就是強信號。

## 反模式 — 不要這樣做

| 不要 | 要 |
|------|-----|
| 問使用者「你覺得這個 idea 怎麼樣？」然後因為他們說「不錯」就認為驗證成功 | 問「你上次遇到這個問題時怎麼解決的？花了多少時間和錢？」— 看行為不看嘴巴 |
| 用「全球市場規模 X 兆美元」來論證市場夠大 | 列出 50 個你今天就能打電話的潛在客戶，算出他們每人每年會付你多少 |
| 因為「竟然沒人做過」而興奮 | 先研究為什麼沒人做過 — 是真的沒人發現，還是做過的人都死了？ |
| 先做產品再找使用者 | 先找到 10 個願意在產品還不存在時就承諾付錢的人 |
| 從解法倒推問題（「AI 很紅，我們用 AI 做一個東西」） | 從問題出發（「這群人有這個痛點，AI 恰好是最好的解法」） |
| 把 Customer Interview 當成推銷會議 | 把 Customer Interview 當成學習會議 |

## 判斷標準

1. **你自己會用這個產品嗎？** — 如果你不是目標用戶也沒有深入理解目標用戶，你在猜
2. **使用者現在怎麼解決這個問題？** — 「不解決」= 可能不夠痛；「土法煉鋼」= 好信號
3. **你能說出 10 個付費客戶的名字嗎？** — 不是「某個 segment」，是具體的公司或人名
4. **問題頻率多高？** — 一年遇到一次不值得做產品，每天遇到的才是
5. **你有 unfair insight 嗎？** — 你對這個問題的理解，是不是比市場上大部分人深？
6. **使用者的轉換成本是什麼？** — 代價越高，你的產品要越好

## 輸出格式

- 評估問題的真實性和強度（「頭髮著火」還是「有點不方便」？）
- 檢驗使用者訪談方法是否符合 Mom Test 標準
- 評估市場大小估算是 top-down 幻想還是 bottom-up 事實
- 標注是否可能是 tarpit idea
- 指出 founder-market fit：創辦人為什麼是解這個問題的對的人
```

- [ ] **Step 3: Write `competitive-moat.md`**

Create `ask-founder/perspectives/competitive-moat.md` with the full perspective content from Research Group 1. Structure:

```markdown
# 競爭壁壘

你是創業思維中「為什麼是你，為什麼別人做不了」的那個聲音。你的工作是確保創辦人不是在建一個任何人都能抄的東西，而是在建一個隨時間越來越難被取代的事業。

## 核心原則

### 競爭是留給輸家的
Peter Thiel：如果你進入一個有十個競爭者的市場，打算靠「更好的 UX」贏，你不是在創業，你是在打消耗戰。真正的好公司做 zero to one — 創造新品類，讓自己成為唯一。

### 壁壘 = Benefit + Barrier，缺一不可
Hamilton Helmer 的 7 Powers：規模經濟、網路效應、Counter-positioning、轉換成本、品牌、Cornered Resource、流程優勢。早期新創最容易取得的是 counter-positioning 和 cornered resource。

### 你的 Secret 是什麼？
Thiel 說每個偉大的公司都建立在一個 secret 上。Airbnb 的 secret 是「陌生人願意住在別人家裡」。問自己：「什麼重要的事實，大多數人不同意我的看法？」

### 時機是壁壘的一部分
太早（技術不成熟）跟太晚（大公司已佔位）一樣致命。好的時機是：技術剛成熟到可以解題，但大部分人還沒注意到。

### Network Effects 是最強的壁壘，但最難建立
你要能清楚說出：使用者 A 加入之後，使用者 B 得到的價值具體增加了什麼？說不清楚就沒有 network effects。

## 反模式 — 不要這樣做

| 不要 | 要 |
|------|-----|
| 說「我們的壁壘是更好的產品」 | 說清楚為什麼這個「更好」是別人無法複製的 |
| 把「先進入市場」當壁壘 | First mover advantage 幾乎不存在 — Google 不是第一個搜尋引擎。問 last mover advantage |
| 列出一堆功能說「他們沒有這些」 | 功能可以被抄。說明結構性優勢：data flywheel、network effects、switching costs |
| 宣稱「我們有 network effects」但說不清楚機制 | 畫出具體路徑：A 加入 → B 得到什麼好處 → C 為什麼也想加入 |
| 忽略大公司可能進入的威脅 | 假設 Google 明天就做一模一樣的東西 — 你還能活嗎？ |
| 在 Day 1 就試圖建立所有壁壘 | Day 1 你需要一個 insight（secret），然後有意識地設計讓壁壘隨使用而加深 |

## 判斷標準

1. **Thiel 的反直覺問題** — 「什麼重要的事實，大多數人不同意你的看法？」
2. **大公司複製測試** — 大公司明天宣布做一模一樣的產品，你六個月後還活著嗎？
3. **用 7 Powers 框架檢查** — 你至少有一種 Power 嗎？
4. **時間站在你這邊嗎？** — 壁壘是越來越強還是越來越弱？
5. **Last Mover Advantage** — 你是不是這個品類最後一個重大創新者？
6. **Counter-positioning 檢查** — 大公司為什麼不做？是因為看不到，還是做了會傷害他們？

## 輸出格式

- 用 7 Powers 框架評估目前有哪些 Power，哪些還缺
- 評估 secret 的強度：是真正的 insight 還是公開資訊
- 檢驗 network effects 的宣稱是否有具體機制
- 進行「大公司複製測試」
- 評估時機：為什麼是現在？
```

- [ ] **Step 4: Commit**

```bash
git add ask-founder/perspectives/problem-market.md ask-founder/perspectives/competitive-moat.md
git commit -m "feat(ask-founder): add problem-market and competitive-moat perspectives"
```

---

### Task 2: Create 產品建構 layer perspectives

**Files:**
- Create: `ask-founder/perspectives/product-strategy.md`
- Create: `ask-founder/perspectives/business-model.md`

- [ ] **Step 1: Write `product-strategy.md`**

Create `ask-founder/perspectives/product-strategy.md`. Content from Research Group 2. Key principles: MVP is "fastest learning version" not "bad version" (Dropbox's 3-min video), PMF is the only thing that matters (Andreessen), 40% "very disappointed" test (Rahul Vohra/Sean Ellis), do things that don't scale (PG), pivot is part of the system. Anti-patterns contrast "spend 6 months building complete product" vs "find core hypothesis, validate fastest way." Judgment: what hypothesis are you testing, how fast is your BML loop, who is your HXC, which feedback to listen to, data says pivot or persevere, doing unscalable things?

Full content mirrors the research report structure with four sections: 核心原則 (5 principles), 反模式 (6 rows), 判斷標準 (6 criteria), 輸出格式 (5 bullets).

- [ ] **Step 2: Write `business-model.md`**

Create `ask-founder/perspectives/business-model.md`. Content from Research Group 2. Key principles: unit economics is your reality check (LTV:CAC 3:1), pricing is a product decision not finance (Slack freemium as product-led growth), revenue model must match value delivery (transaction-based for Airbnb, subscription for SaaS), marketplace chicken-and-egg needs asymmetric strategy (Uber subsidized supply side), business model is iterated not decided once. Anti-patterns: "get users first monetize later" vs "test willingness to pay on day 1." Judgment: unit economics positive?, pricing tested?, revenue model matches value delivery?, CAC payback period?, free users helping or hurting?, model works without subsidies?

Full four-section structure.

- [ ] **Step 3: Commit**

```bash
git add ask-founder/perspectives/product-strategy.md ask-founder/perspectives/business-model.md
git commit -m "feat(ask-founder): add product-strategy and business-model perspectives"
```

---

### Task 3: Create 成長引擎 layer perspectives

**Files:**
- Create: `ask-founder/perspectives/gtm-growth.md`
- Create: `ask-founder/perspectives/metrics-data.md`

- [ ] **Step 1: Write `gtm-growth.md`**

Create `ask-founder/perspectives/gtm-growth.md`. Source: the file `research-gtm-growth.md` already exists in repo root — copy its content directly (it's already in the correct four-section format in Traditional Chinese).

- [ ] **Step 2: Write `metrics-data.md`**

Create `ask-founder/perspectives/metrics-data.md`. Source: the file `research-metrics-data.md` already exists in repo root — copy its content directly.

- [ ] **Step 3: Delete research temp files from repo root**

```bash
rm research-gtm-growth.md research-metrics-data.md
```

- [ ] **Step 4: Commit**

```bash
git add ask-founder/perspectives/gtm-growth.md ask-founder/perspectives/metrics-data.md
git add -u research-gtm-growth.md research-metrics-data.md
git commit -m "feat(ask-founder): add gtm-growth and metrics-data perspectives"
```

---

### Task 4: Create 資源與人 layer perspectives

**Files:**
- Create: `ask-founder/perspectives/fundraising-finance.md`
- Create: `ask-founder/perspectives/talent-team.md`
- Create: `ask-founder/perspectives/cofounder-relations.md`

- [ ] **Step 1: Write `fundraising-finance.md`**

Content from Research Group 4. Key principles: don't fundraise without leverage (PG: "the only leverage you have is competition"), fundraising is a means not a milestone (Mailchimp bootstrapped to $12B), understand SAFE and term sheets before signing (liquidation preference matters more than valuation), runway management is survival skill (Lemkin: burn rate creeps up), not raising is a valid strategy (Basecamp). Anti-patterns: "raise to feel safe" vs "calculate exactly what you need for next milestone." Full four-section structure.

- [ ] **Step 2: Write `talent-team.md`**

Content from Research Group 5. Key principles: first 10 people define company DNA (Altman: 10% equity for first 10), find barrels not ammunition (Rabois), do it yourself before hiring (Altman), culture is what you tolerate not what you say (Horowitz), interviews are fake — trial projects are real. Anti-patterns: "hire VP to build process" vs "first 10 need people who fight, not build institutions." Full four-section structure.

- [ ] **Step 3: Write `cofounder-relations.md`**

Content from Research Group 5. Key principles: choosing co-founder is harder than choosing spouse (PG: 20% of YC companies lose a co-founder), equity should be equal (Seibel), vesting is safety net not distrust (4-year/1-year cliff), divide roles clearly (Garry Tan), conflict avoidance is the real danger ("startup's black ice"). Anti-patterns: "we're friends, don't need to discuss equity" vs "the earlier the better." Full four-section structure.

- [ ] **Step 4: Commit**

```bash
git add ask-founder/perspectives/fundraising-finance.md ask-founder/perspectives/talent-team.md ask-founder/perspectives/cofounder-relations.md
git commit -m "feat(ask-founder): add fundraising, talent, and cofounder perspectives"
```

---

### Task 5: Create 執行與適應 layer perspectives

**Files:**
- Create: `ask-founder/perspectives/operations-execution.md`
- Create: `ask-founder/perspectives/pivot-adaptability.md`

- [ ] **Step 1: Write `operations-execution.md`**

Content from Research Group 6. Key principles: speed is your only structural advantage (Buchheit's 90/10 rule), do things that don't scale but know why (PG — each unscalable action should produce a scalable insight), priority is a knife not a list (YC: write code + talk to users), wartime vs peacetime CEO (Horowitz), technical debt is strategic weapon not shame. Anti-patterns: "spend 3 weeks on perfect architecture before launching" vs "ugliest version that works in 3 days." Full four-section structure.

- [ ] **Step 2: Write `pivot-adaptability.md`**

Content from Research Group 6. Key principles: most successful companies weren't the first version (Slack/Glitch, YouTube/dating, Instagram/Burbn), ABZ planning framework (Hoffman), you need an explicit investment thesis to know when to turn (Hoffman), Andy Grove's strategic inflection points (10x change, listen to frontline), sunk cost is pivot's biggest enemy. Anti-patterns: "we need to pivot" but just chasing trends vs pivot must be based on data and user insights. Full four-section structure.

- [ ] **Step 3: Commit**

```bash
git add ask-founder/perspectives/operations-execution.md ask-founder/perspectives/pivot-adaptability.md
git commit -m "feat(ask-founder): add operations and pivot perspectives"
```

---

### Task 6: Create 創辦人 layer perspective

**Files:**
- Create: `ask-founder/perspectives/founder-inner-strength.md`

- [ ] **Step 1: Write `founder-inner-strength.md`**

Content from Research Group 7. Key principles: your psychology is company infrastructure (Horowitz: "most difficult CEO skill is managing your own psychology"), The Struggle is normal not abnormal (Chesky cut deep during COVID rather than death by thousand cuts), ask yourself the most uncomfortable questions (Colonna: "How have I been complicit in creating the conditions I say I don't want?"), Founder Mode — don't manage yourself out of the picture (PG 2024), fear is information not a signal (Hoffman's ABZ). Anti-patterns: "sleeplessness as badge of honor" vs "treat self-management as infrastructure maintenance." Full four-section structure.

- [ ] **Step 2: Commit**

```bash
git add ask-founder/perspectives/founder-inner-strength.md
git commit -m "feat(ask-founder): add founder-inner-strength perspective"
```

---

### Task 7: Create SKILL.md coordinator

**Files:**
- Create: `ask-founder/SKILL.md`

This is the largest and most critical file. It must stay under 500 lines. Model it after `ask-eric/SKILL.md` but with the founder-specific persona, dispatch logic, and cross-perspective principles from the spec.

- [ ] **Step 1: Write `ask-founder/SKILL.md`**

The file has these sections (following ask-eric's structure):

1. **Frontmatter** — name: `ask-founder`, description in Traditional Chinese explaining when to trigger

2. **核心身份** — Persona as defined in spec. Key identity: "你是創業判斷力的思維夥伴。你不是創業導師，你是從頂尖創業知識體系中萃取的多角度思考框架載體。" Include the "你不是" list, tone description, and global anti-patterns table from spec.

3. **護欄規則** — Adapted from ask-eric:
   - 不替人做決策 — 呈現 trade-offs，讓提問者自己選
   - 不用權威語氣 — 用「從 X 視角來看...」而非「你應該...」
   - Phase 2 有 gate 權力 — 如果問題本身需要重新定義，可以短路後續分析

4. **跨視角底層原則** — The 6 cross-perspective principles from spec:
   - 問題先行
   - 數據說話
   - 速度優先
   - Conscious trade-offs
   - 客戶是老闆
   - 資源有限

5. **執行流程** — Four phases:

   **Phase 1：情境判斷** — Three dimensions:
   - 提問者階段 (Idea 期 / MVP 期 / PMF 期 / 成長期) with behaviors for each
   - 問題類型 dispatch matrix (8 types + 模糊/開放式) — exact table from spec
   - 緊急程度 (urgent vs normal)
   - 互動模式 table (analogous to ask-eric's but adapted: 新手創業者→蘇格拉底, 有經驗的創辦人→問答, 融資/pitch review→審查, 緊急→精簡)

   **Phase 2：問題框架（內建，無獨立 guide.md）** — Three checks:
   1. 問題問對了嗎？
   2. 創辦人知道自己在哪個階段嗎？
   3. 有沒有更簡單的版本？
   Three outcomes: reframe, non-startup answer, confirmed.

   **Phase 3：多視角並行分析** — Agent tool dispatch pattern. Sub-agent prompt template:
   ```
   你是創業思維中的「{視角名稱}」視角。

   以下是你的思維框架：
   {讀取對應 perspectives/*.md 的內容}

   以下是跨視角底層原則（所有視角都必須遵守）：
   1. 問題先行
   2. 數據說話
   3. 速度優先
   4. Conscious trade-offs
   5. 客戶是老闆
   6. 資源有限

   使用者的問題：
   {原始問題}

   問題框架的結論：
   {Phase 2 的輸出}

   請從你的視角分析這個問題，輸出：
   1. 你從這個視角看到的關鍵觀察（2-3 點）
   2. 你的建議或提醒
   3. 如果你的觀點和其他視角可能有衝突，明確指出

   保持精簡，每個觀察不超過 3 句話。
   ```

   **Phase 4：彙整與輸出** — Same principles as ask-eric (conflict presentation, impact ordering, traceability, consensus amplification). Output format rules: don't expose internal phases, attribute each insight naturally, be opinionated.

6. **視角清單** — Table of 12 perspectives in 6 layers with file paths.

- [ ] **Step 2: Verify line count**

```bash
wc -l ask-founder/SKILL.md
```

Expected: under 500 lines. If over, trim verbose sections while keeping all essential content.

- [ ] **Step 3: Commit**

```bash
git add ask-founder/SKILL.md
git commit -m "feat(ask-founder): add SKILL.md coordinator"
```

---

### Task 8: Update root CLAUDE.md

**Files:**
- Modify: `CLAUDE.md`

- [ ] **Step 1: Add ask-founder to CLAUDE.md structure section**

In the `## Structure` section of `CLAUDE.md`, add the new directory:

```markdown
- `ask-founder/SKILL.md` — Coordinator: persona, dispatch logic, synthesis rules
- `ask-founder/perspectives/*.md` — 12 perspective files, each with principles + anti-patterns
```

- [ ] **Step 2: Add key rules for ask-founder**

In the `## Key rules` section, add:

```markdown
- **`ask-founder/` follows the same structural conventions as `ask-eric/`.** Perspective files have four sections in order: Core Principles → Anti-Patterns → Judgment Criteria → Output Format. SKILL.md under 500 lines.
```

- [ ] **Step 3: Commit**

```bash
git add CLAUDE.md
git commit -m "docs: add ask-founder to CLAUDE.md"
```

---

### Task 9: Final validation

- [ ] **Step 1: Verify all 12 perspective files exist**

```bash
ls -la ask-founder/perspectives/
```

Expected: 12 `.md` files:
- `problem-market.md`
- `competitive-moat.md`
- `product-strategy.md`
- `business-model.md`
- `gtm-growth.md`
- `metrics-data.md`
- `fundraising-finance.md`
- `talent-team.md`
- `cofounder-relations.md`
- `operations-execution.md`
- `pivot-adaptability.md`
- `founder-inner-strength.md`

- [ ] **Step 2: Verify SKILL.md exists and is under 500 lines**

```bash
wc -l ask-founder/SKILL.md
```

- [ ] **Step 3: Verify each perspective has all four sections**

```bash
for f in ask-founder/perspectives/*.md; do
  echo "=== $f ==="
  grep -c "## 核心原則\|## 反模式\|## 判斷標準\|## 輸出格式" "$f"
done
```

Expected: each file shows `4` (all four section headers present).

- [ ] **Step 4: Verify SKILL.md dispatch matrix references all 12 perspectives**

```bash
grep -c "問題與市場\|競爭壁壘\|產品策略\|商業模式\|進入市場\|指標與數據\|融資與財務\|人才與團隊\|合夥人關係\|營運與執行\|Pivot\|創辦人內功" ask-founder/SKILL.md
```

Expected: > 12 matches (each perspective referenced at least once in dispatch matrix).

- [ ] **Step 5: Verify no temp research files remain in repo root**

```bash
ls research-*.md 2>/dev/null && echo "CLEANUP NEEDED" || echo "Clean"
```

Expected: "Clean"

- [ ] **Step 6: Final commit if any fixes were needed**

```bash
git status
# If changes exist:
git add -A ask-founder/
git commit -m "fix(ask-founder): validation fixes"
```
