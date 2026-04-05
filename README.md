# Prism

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/github/v/tag/ceparadise168/prism?label=version)](https://github.com/ceparadise168/prism/releases)

One question in, multiple perspectives out.

Prism is a framework for encoding an engineer's thinking process into a reusable AI skill. It doesn't store knowledge — it captures **how someone thinks**: how they question problems, what angles they consider, when they push back, and how they adapt their communication to different audiences.

## Why

When a senior engineer leaves a team, their code stays but their judgment leaves. Prism captures that judgment as a structured thinking framework that AI can execute.

## How It Works

```
User asks a question
       |
       v
  Guide Perspective (gate power)
  "Is this the right question?"
       |
       +-- Reframe --> ask user to reconsider
       +-- No tech needed --> non-technical advice
       +-- Confirmed --> continue
       |
       v
  Dispatch relevant perspectives (parallel)
  [architecture] [quality] [security] [pragmatic] [...]
       |
       v
  Synthesize with interaction mode
  (Socratic / Q&A / Review / Concise)
       |
       v
  Multi-perspective response
```

Key design decisions:
- **Guide perspective has gate power** — it can short-circuit all analysis if the question itself needs reframing
- **Interaction mode adapts to the audience** — Socratic for juniors, Q&A for peers, de-technicalized for PMs
- **Perspectives have anti-patterns** — each perspective knows what "generic AI advice" looks like and avoids it

## Output Examples

<details>
<summary><b>Peer engineer asks: "Should we use Kafka or SQS?"</b></summary>

> Input: "我們的即時累點系統現在用 polling 每 5 秒去撈一次 CRM API，延遲太高了，想改成 event-driven。目前有在考慮用 Kafka 或是 AWS SQS，你覺得呢？"

**Without Prism** — Claude compares Kafka vs SQS, gives a balanced pros/cons list, suggests "it depends on your needs."

**With Prism** — the skill:
1. **Questions the premise first**: "你說延遲太高，高到什麼程度算問題？5 秒在 App 顯示點數 vs 5 秒內推播通知，嚴重程度差很多"
2. **Expands the option space**: adds Webhook+Queue, EventBridge, Database CDC, and polling optimization — not just the two options the user mentioned
3. **States a clear preference**: "我偏好 SQS。不要因為 Kafka 比較專業就選 Kafka。" — with specific reasoning about team capability and operational overhead
4. **Warns about hidden costs**: DLQ, idempotency, schema versioning, and "event-driven 的 debugging 難度會上升"
5. **Gives a stakeholder pitch**: "17,280 次無效 API call/天 → 降到實際事件數量"

</details>

<details>
<summary><b>Someone asks: "Boss says we're too slow, what should I do?"</b></summary>

> Input: "老闆覺得我們的開發速度太慢了，要我想辦法加速，你覺得該怎麼辦？"

**Without Prism** — Claude says "先診斷根本原因" then immediately lists 5 categories of solutions (requirements, tech debt, process, planning, tooling).

**With Prism** — the guide perspective **fires its gate power**:

> "等一下。在你衝去優化 CI/CD、推 Scrum、買 Copilot 之前，我想先質疑這個問題本身。「開發速度太慢」這句話，問題問錯了。這是一個症狀描述，不是問題定義。"

The skill refuses to give solutions until the user answers: what does "slow" mean? Measured how? Compared to what? Then provides a concrete first step: "Make Work Visible — 追蹤最近 3-5 個 feature 的生命週期，找出時間花在哪裡。"

</details>

<details>
<summary><b>Junior asks for a code review (Socratic mode)</b></summary>

> Input: A junior engineer shares their first API endpoint (with SQL injection, missing validation, incorrect null checks)

**Without Prism** — Claude lists all 6 issues, provides corrected code, and says "有問題隨時可以再討論！"

**With Prism** — switches to Socratic mode automatically. Instead of listing issues, it asks:

> "如果有人傳這個進來，會發生什麼？"
> ```
> memberId: "1' OR '1'='1"
> ```
> "把它帶入你的 SQL 字串，看看組出來的 query 長什麼樣子。你發現什麼了嗎？"

No fixed code. No direct answers. 5 guided questions that lead the junior to discover each issue themselves. Ends with: "你覺得哪個問題最值得先深入？"

</details>

<details>
<summary><b>Tech lead faces interpersonal + technical conflict</b></summary>

> Input: "Senior 堅持用 MongoDB 做訂單系統，但我覺得 PostgreSQL 比較適合。他資歷比我深，每次開會提反對意見他就不太高興。"

**Without Prism** — Claude gives technical comparison + generic "建議保持專業、開放溝通、用數據說話"

**With Prism** — reframes the problem and simulates the Senior's reaction:

> "你真正的問題不是 MongoDB vs PostgreSQL，是怎麼在資歷壓制的環境裡推動正確的技術決策。"
>
> "如果我是那個 Senior，有人說『我覺得 PostgreSQL 比較適合』，我的第一個反應不是『他說的對不對』，而是『他是在挑戰我，還是在貢獻討論？』"

Gives a specific action plan: write a one-page technical analysis, share it privately before the meeting, frame it as "我想聽你對這幾個疑問的看法" instead of "我反對."

Cross-perspective consensus: "你的問題是你的論點不夠強，而不是你說話的機會不夠多。先武裝自己，再選擇戰場。"

</details>

## 20 Perspectives, 8 Layers

| Layer | Perspectives | Core Question |
|-------|-------------|---------------|
| Problem Definition | Guide, User Story | Is this the right question? |
| Solution Exploration | Research | What are the options? |
| Technical Depth | Root Cause, Architecture, Quality, Security, Methodology, Maintenance | How to do it right? |
| System Runtime | Observability, Incident Response | Can we see it? What if it breaks? |
| Change Execution | Change Execution | Dependencies, rollback, verification, notification? |
| System Value | Data, Operations, Customer Experience | Does it create a flywheel? |
| Execution & Advocacy | Pragmatic, Project Management, Value Narrative, Interpersonal | Can we ship it? Can we get buy-in? |
| Sustainability | Governance | Can it live and grow? |

## Quick Start

### Use with Claude Code

```bash
# Clone the repo
git clone https://github.com/ceparadise168/prism.git

# Install the skill
claude skill install ./prism/ask-eric
```

Then in any Claude Code session:

```
/ask-eric 我們打算把 monolith 拆成 microservices，團隊只有 5 個人，你怎麼看？
```

### Use with Any LLM (ChatGPT, Gemini, etc.)

Copy the content of `eric-engineering-mind.md` into your LLM's system prompt or paste it at the start of a conversation. Then ask your question.

### Create Your Own Prism

See [CONTRIBUTING.md](CONTRIBUTING.md) for a step-by-step guide.

## Example: `ask-eric`

The included `ask-eric/` directory is a complete Prism instance — a digital twin of Eric's engineering mindset. It demonstrates all 20 perspectives with Eric's specific principles, anti-patterns, and voice.

```
/ask-eric 我們打算把 monolith 拆成 microservices，團隊只有 5 個人，你怎麼看？
```

The skill will:
1. Question whether 5 people can sustain microservices (guide perspective)
2. Analyze the architecture trade-offs (architecture perspective)
3. Challenge the premise with team context (pragmatic perspective)
4. Warn about operational complexity (operations perspective)
5. Synthesize into an opinionated, concrete response

## Universal Version

`eric-engineering-mind.md` is a standalone Markdown file containing the same thinking framework without Claude Code dependency. Feed it to any LLM as a system prompt.

## Project Structure

```
prism/
├── ask-eric/                      # Example Prism instance
│   ├── SKILL.md                   # Coordinator (persona + dispatch + synthesis)
│   ├── perspectives/              # 20 perspective files
│   │   ├── guide.md               # Gate power — question the question
│   │   ├── user-story.md          # JTBD and Design Thinking
│   │   ├── research.md            # Multi-option trade-off analysis
│   │   ├── root-cause.md          # Causal chain tracing
│   │   ├── architecture.md        # Simple, scalable, extensible
│   │   ├── quality.md             # Naming, cognitive load, clean code
│   │   ├── security.md            # OWASP, boundary validation
│   │   ├── methodology.md         # TDD as design tool, architecture patterns
│   │   ├── maintenance.md         # Tech debt, handoff experience
│   │   ├── observability.md       # Logging, metrics, tracing
│   │   ├── incident-response.md   # Stop bleeding, blameless postmortem
│   │   ├── change-execution.md   # Dependencies, rollback, verification, notification
│   │   ├── data.md                # Data quality, decision support
│   │   ├── operations.md          # Closed loop, flywheel
│   │   ├── customer-experience.md # JTBD, experience consistency
│   │   ├── pragmatic.md           # Context-driven decisions
│   │   ├── project-management.md  # Decomposition, incremental delivery
│   │   ├── value-narrative.md     # ROI, stakeholder communication
│   │   ├── interpersonal.md       # Read the room, simulate reactions
│   │   └── governance.md          # API/arch/security/ops governance
│   └── README.md                  # Installation and usage
├── eric-engineering-mind.md       # Universal version (any LLM)
├── docs/                          # Design specs and test reports
├── LICENSE                        # MIT
└── README.md                      # This file
```

## License

MIT
