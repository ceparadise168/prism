# Prism — Agent Instructions

## What is this project?

Prism is a framework for encoding judgment into reusable AI skills. `ask-eric/` is the reference implementation (engineering judgment). `ask-founder/` encodes entrepreneurship judgment from top startup knowledge sources.

## Structure

- `plugins/prism/skills/ask-eric/SKILL.md` — Coordinator: persona, dispatch logic, synthesis rules
- `plugins/prism/skills/ask-eric/perspectives/*.md` — 20 perspective files, each with principles + anti-patterns
- `plugins/prism/skills/ask-founder/SKILL.md` — Coordinator: persona, dispatch logic, synthesis rules
- `plugins/prism/skills/ask-founder/perspectives/*.md` — 12 perspective files, each with principles + anti-patterns
- `eric-engineering-mind.md` — Standalone version for non-Claude-Code LLMs
- `docs/` — Design specs and validation artifacts (internal, not part of the skill)

## Key rules

- **Don't modify perspective content without understanding the anti-patterns.** Each perspective has a "don't do this / do this" section that prevents generic output. Respect it.
- **Keep SKILL.md under 500 lines.** Progressive disclosure: heavy content goes in perspective files, SKILL.md is the coordinator.
- **Perspective files follow a consistent structure:** Core Principles → Anti-Patterns → Judgment Criteria → Output Format (all perspectives in both `plugins/prism/skills/ask-eric/` and `plugins/prism/skills/ask-founder/` have all four sections, in this order)
- **Test changes with real questions.** Run at least 2-3 diverse questions through the skill before committing. Compare with baseline (without skill) to verify the skill adds value.
- **Keep validation claims honest.** `ask-eric` is the documented reference implementation; `ask-founder` is included in the plugin, but published evaluation evidence is currently lighter unless equivalent eval artifacts are added.
- **Language:** `ask-eric/` and `ask-founder/` content is in Traditional Chinese. Root-level docs are in English.

## When editing perspectives

1. Read the existing content first
2. Check the anti-patterns section — make sure your changes don't violate them
3. Be concrete and opinionated, not abstract and neutral
4. If adding a new principle, add a corresponding anti-pattern
