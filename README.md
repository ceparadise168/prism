# Prism

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/github/v/tag/ceparadise168/prism?label=version)](https://github.com/ceparadise168/prism/releases)

**[繁體中文](README.zh-TW.md)**

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

Since `ask-eric` responds in Traditional Chinese, quotes below are shown in the original language with English summaries.

<details>
<summary><b>Peer engineer asks: "Should we use Kafka or SQS?"</b></summary>

> Input: "Our loyalty points system polls the CRM API every 5 seconds. Latency is too high — we want to switch to event-driven. Thinking Kafka or SQS. What do you think?"

**Without Prism** — Claude compares Kafka vs SQS, gives a balanced pros/cons list, suggests "it depends on your needs."

**With Prism** — the skill:
1. **Questions the premise first**: "You say latency is too high — how high is too high? 5 seconds for displaying points in-app vs. 5 seconds for push notifications are very different severity levels."
2. **Expands the option space**: adds Webhook+Queue, EventBridge, Database CDC, and polling optimization — not just the two options the user mentioned
3. **States a clear preference**: "I'd go with SQS. Don't pick Kafka just because it sounds more serious." — with specific reasoning about team capability and operational overhead
4. **Warns about hidden costs**: DLQ, idempotency, schema versioning, and "debugging gets harder once you go event-driven"
5. **Gives a stakeholder pitch**: "17,280 wasted API calls/day reduced to actual event count"

</details>

<details>
<summary><b>Someone asks: "Boss says we're too slow, what should I do?"</b></summary>

> Input: "My boss thinks our dev velocity is too slow and wants me to speed things up. What should I do?"

**Without Prism** — Claude says "diagnose the root cause first" then immediately lists 5 categories of solutions (requirements, tech debt, process, planning, tooling).

**With Prism** — the guide perspective **fires its gate power**:

> "Hold on. Before you rush off to optimize CI/CD, push Scrum, or buy Copilot — I want to question the problem itself. 'Development is too slow' is a symptom description, not a problem definition."

The skill refuses to give solutions until the user answers: what does "slow" mean? Measured how? Compared to what? Then provides a concrete first step: "Make Work Visible — track the lifecycle of the last 3-5 features and find out where the time actually goes."

</details>

<details>
<summary><b>Junior asks for a code review (Socratic mode)</b></summary>

> Input: A junior engineer shares their first API endpoint (with SQL injection, missing validation, incorrect null checks)

**Without Prism** — Claude lists all 6 issues, provides corrected code, and says "Feel free to ask if you have questions!"

**With Prism** — switches to Socratic mode automatically. Instead of listing issues, it asks:

> "What happens if someone sends this?"
> ```
> memberId: "1' OR '1'='1"
> ```
> "Substitute it into your SQL string and look at the resulting query. What do you see?"

No fixed code. No direct answers. 5 guided questions that lead the junior to discover each issue themselves. Ends with: "Which of these issues do you think is worth digging into first?"

</details>

<details>
<summary><b>Tech lead faces interpersonal + technical conflict</b></summary>

> Input: "A senior engineer insists on using MongoDB for our order system, but I think PostgreSQL is a better fit. He's more experienced than me and gets annoyed whenever I push back in meetings."

**Without Prism** — Claude gives technical comparison + generic "stay professional, communicate openly, use data"

**With Prism** — reframes the problem and simulates the Senior's reaction:

> "Your real problem isn't MongoDB vs PostgreSQL — it's how to drive the right technical decision in an environment with seniority dynamics."
>
> "If I were that Senior and someone said 'I think PostgreSQL is better,' my first reaction wouldn't be 'is he right?' — it would be 'is he challenging me, or contributing to the discussion?'"

Gives a specific action plan: write a one-page technical analysis, share it privately before the meeting, frame it as "I'd like to hear your thoughts on these questions" instead of "I disagree."

Cross-perspective consensus: "Your problem is that your argument isn't strong enough, not that you don't get enough airtime. Arm yourself first, then pick your battlefield."

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

**Option A: Personal install (available in all your projects)**

```bash
git clone https://github.com/ceparadise168/prism.git
cp -r prism/ask-eric ~/.claude/skills/ask-eric
```

**Option B: Project install (shared with your team via git)**

```bash
git clone https://github.com/ceparadise168/prism.git
cp -r prism/ask-eric .claude/skills/ask-eric
# then commit .claude/skills/ask-eric/ to your repo
```

**Option C: Symlink (auto-sync with upstream)**

```bash
git clone https://github.com/ceparadise168/prism.git ~/prism
ln -s ~/prism/ask-eric ~/.claude/skills/ask-eric
```

After installation, restart Claude Code. The skill is auto-discovered — type `/` and look for `ask-eric`:

```
/ask-eric We're planning to split our monolith into microservices. Team of 5. What do you think?
```

**Verify it works:**

```
/ask-eric hello
```

You should get a response in Eric's voice (in Traditional Chinese), not generic Claude output.

**Uninstall:**

```bash
rm -rf ~/.claude/skills/ask-eric     # personal install
rm -rf .claude/skills/ask-eric       # project install
```

**Update:**

```bash
cd ~/prism && git pull                          # if you used symlink (Option C)
cp -r ~/prism/ask-eric ~/.claude/skills/ask-eric  # if you used copy (Option A)
```

### Use with Any LLM (ChatGPT, Gemini, etc.)

Copy the content of [`eric-engineering-mind.md`](eric-engineering-mind.md) into your LLM's system prompt, or paste it at the start of a conversation. Then ask your question normally — no slash command needed.

### Create Your Own Prism

See [CONTRIBUTING.md](CONTRIBUTING.md) for a step-by-step guide.

## Example: `ask-eric`

The included `ask-eric/` directory is a complete Prism instance — a digital twin of Eric's engineering mindset. It demonstrates all 20 perspectives with Eric's specific principles, anti-patterns, and voice.

```
/ask-eric We want to break our monolith into microservices. Team of 5. Thoughts?
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
