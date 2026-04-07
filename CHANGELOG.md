# Changelog

## [1.3.0] - 2026-04-07

### Added
- `ask-founder` entrepreneurship skill with 12 perspective files and a dedicated coordinator
- Slash command entry points for `ask-eric` and `ask-founder`
- Marketplace-compatible plugin packaging under `plugins/prism/`
- Asciinema demo in the root README

### Changed
- Repository structure updated to support installable Claude Code plugin workflows
- Root documentation split into English and Traditional Chinese READMEs
- Contributor guidance aligned with the packaged `plugins/prism/skills/` layout
- Validation status is now documented more explicitly: `ask-eric` is the reference implementation, while `ask-founder` is included with lighter published evaluation evidence

### Fixed
- Broken and misleading extension-path guidance in `CONTRIBUTING.md`
- Broken non-Claude-Code reference in `plugins/prism/skills/ask-eric/README.md`
- Release notes now match the plugin manifests that already declared `1.3.0`

## [1.1.0] - 2026-04-06

### Added
- Change Execution perspective (#20) — dependency sequencing, migration strategy, rollback at every step, post-execution verification, notification obligations
- Data protection section in security perspective — PII compliance, de-identification, hash-based third-party exchange, implicit leakage prevention (auto-increment ID, predictable sequences, API over-sharing)
- Third-party vendor management in governance perspective — contracts, contact windows, key rotation, whitelists, authentication, authorization, disconnection response, data flow

### Changed
- OWASP Top 10 updated from 2021 to 2025 (Supply Chain Failures, Mishandling of Exceptional Conditions, SBOM)
- All 20 perspective files unified to consistent section ordering: Core Principles → Anti-Patterns → Judgment Criteria → Output Format
- Anti-patterns expanded from 6 to all 20 perspectives

### Fixed
- Stale references: 19→20 perspectives, 7→8 layers across all files
- Duplicate layer numbering in eric-engineering-mind.md
- Sub-agent prompt template missing principles #6 and #7
- CLAUDE.md structure description now matches actual file structure

## [1.0.0] - 2026-04-06

### Added
- Prism framework with 20 perspectives across 8 layers
- `ask-eric` as the reference Prism instance
- `eric-engineering-mind.md` universal version for any LLM
- Guide perspective with gate power (can short-circuit analysis)
- 4 interaction modes: Socratic, Q&A, Review, Concise
- Dispatch matrix mapping question types to perspective subsets
- Anti-patterns in SKILL.md and all 20 perspectives
- Cross-perspective principles: industry standards first, API first, standardize for leverage, design for reuse, acceptance criteria first, 12-Factor App, ISO 27001

### Tested
- 6 test cases across 3 iterations
- Scenarios: technical decision, vague management question, junior code review, PM communication, production incident, interpersonal conflict
- Dispatch stability: 3/3 consistent on core logic
