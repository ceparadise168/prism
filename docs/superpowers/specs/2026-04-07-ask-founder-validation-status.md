# Ask Founder — Validation Status

## Summary

`ask-founder` is included in the Prism plugin and is structurally complete:

- 1 coordinator file: `plugins/prism/skills/ask-founder/SKILL.md`
- 12 perspective files under `plugins/prism/skills/ask-founder/perspectives/`
- 1 command entry point: `plugins/prism/commands/ask-founder.md`

## Current Validation State

Compared with `ask-eric`, the published validation evidence for `ask-founder` is currently lighter.

What exists today:

- Design spec: `docs/superpowers/specs/2026-04-06-founder-prism-design.md`
- Implemented coordinator and perspective files in the plugin
- Root README and plugin packaging that expose `ask-founder` as part of Prism

What is not yet published in this repo at the same level as `ask-eric`:

- A dedicated evaluation report comparing `with-skill` vs `without-skill`
- A documented stability check for dispatch consistency
- A comparable set of example test scenarios with findings and iteration notes

## Practical Interpretation

Users should read the current state as:

- `ask-eric`: reference implementation with documented evaluation artifacts
- `ask-founder`: available for use, but not yet backed by equally detailed published eval documentation

This is a documentation honesty issue, not a claim that `ask-founder` is unusable. The goal is to distinguish structural completeness from validation completeness.

## Suggested Next Step

If Prism wants to present `ask-founder` as equally validated, add a dedicated test analysis report mirroring the structure of `2026-04-05-ask-eric-test-analysis-report.md`.
