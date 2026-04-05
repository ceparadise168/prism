# Prism

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

## 19 Perspectives, 7 Layers

| Layer | Perspectives | Core Question |
|-------|-------------|---------------|
| Problem Definition | Guide, User Story | Is this the right question? |
| Solution Exploration | Research | What are the options? |
| Technical Depth | Root Cause, Architecture, Quality, Security, Methodology, Maintenance | How to do it right? |
| System Runtime | Observability, Incident Response | Can we see it? What if it breaks? |
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

The included `ask-eric/` directory is a complete Prism instance — a digital twin of Eric's engineering mindset. It demonstrates all 19 perspectives with Eric's specific principles, anti-patterns, and voice.

```
/ask-eric 我們打算把 monolith 拆成 microservices，團隊只有 5 個人，你怎麼看？
```

The skill will:
1. Question whether 5 people can sustain microservices (guide perspective)
2. Analyze the architecture trade-offs (architecture perspective)
3. Challenge the premise with team context (pragmatic perspective)
4. Warn about operational complexity (operations perspective)
5. Synthesize into an opinionated, concrete response

## Create Your Own Prism

1. **Fork this repo**
2. **Edit `perspectives/`** — rewrite each perspective with your own principles, judgment criteria, and anti-patterns
3. **Edit `SKILL.md`** — update the persona, voice guidelines, and dispatch matrix
4. **Test** — run real questions through it and iterate

The framework is the structure. Your engineering wisdom is the content.

## Universal Version

`eric-engineering-mind.md` is a standalone Markdown file containing the same thinking framework without Claude Code dependency. Feed it to any LLM as a system prompt.

## Project Structure

```
prism/
├── ask-eric/                      # Example Prism instance
│   ├── SKILL.md                   # Coordinator (persona + dispatch + synthesis)
│   ├── perspectives/              # 19 perspective files
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
