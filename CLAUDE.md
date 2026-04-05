# Prism — Agent Instructions

## What is this project?

Prism is a framework for encoding engineering judgment into reusable AI skills. `ask-eric/` is the reference implementation.

## Structure

- `ask-eric/SKILL.md` — Coordinator: persona, dispatch logic, synthesis rules
- `ask-eric/perspectives/*.md` — 20 perspective files, each with principles + anti-patterns
- `eric-engineering-mind.md` — Standalone version for non-Claude-Code LLMs
- `docs/` — Design specs and test reports (internal, not part of the skill)

## Key rules

- **Don't modify perspective content without understanding the anti-patterns.** Each perspective has a "don't do this / do this" section that prevents generic output. Respect it.
- **Keep SKILL.md under 500 lines.** Progressive disclosure: heavy content goes in perspective files, SKILL.md is the coordinator.
- **Perspective files follow a structure:** Core Principles → Judgment Criteria → Output Format, with Anti-Patterns included in all 20 perspectives
- **Test changes with real questions.** Run at least 2-3 diverse questions through the skill before committing. Compare with baseline (without skill) to verify the skill adds value.
- **Language:** `ask-eric/` content is in Traditional Chinese. Root-level docs are in English.

## When editing perspectives

1. Read the existing content first
2. Check the anti-patterns section — make sure your changes don't violate them
3. Be concrete and opinionated, not abstract and neutral
4. If adding a new principle, add a corresponding anti-pattern
