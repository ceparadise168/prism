# Prism Remediation Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Fix the repo-level delivery gaps that currently prevent Prism from reliably achieving its published goals as an installable, trustable, and extensible Claude Code plugin.

**Architecture:** This is a documentation-and-manifest remediation pass, not a product redesign. The work should align published claims, contributor instructions, plugin metadata, and validation evidence so the repo tells one coherent story: what Prism is, how to install it, how to extend it, and what has actually been validated.

**Tech Stack:** Markdown docs, Claude Code plugin manifests (`.json`), repository structure, shell verification with `rg`, `sed`, and `test`.

## Report

### Objective

Prism already demonstrates a strong concept for `ask-eric`: a multi-perspective judgment framework with meaningful prompt structure, perspective decomposition, and internal evaluation artifacts. The current weaknesses are not primarily in prompt quality. They are in delivery integrity.

The repo currently undershoots its stated goal in four places:

1. The "create your own Prism" contribution path is internally inconsistent.
2. Version metadata and changelog history are out of sync.
3. The non-Claude-Code entry point in `plugins/prism/skills/ask-eric/README.md` is broken.
4. The repo markets both `ask-eric` and `ask-founder` as part of the same finished product, but only `ask-eric` has visible validation evidence.

### Intended Outcome

After this remediation:

1. A contributor with zero prior context can follow the docs and successfully create a custom Prism instance without guessing the repo structure.
2. A user can trust the version number shown in the plugin metadata because it matches documented release history.
3. A user following the non-Claude-Code path lands on a valid, readable universal prompt file.
4. The repo makes an honest, evidence-backed claim about what has and has not been validated.

## Acceptance Standards

### Product-Level Acceptance Criteria

1. All installation, extension, and universal-usage instructions point to real files and real repo structure.
2. The published plugin version and the top entry in `CHANGELOG.md` describe the same release state.
3. The contribution guide does not describe nonexistent manifest behavior.
4. Claims about evaluation are explicit per skill:
   - `ask-eric`: validated with linked evidence
   - `ask-founder`: either validated with linked evidence or clearly labeled as designed-but-not-yet-evaluated
5. No user-facing doc contains obvious mojibake or corrupted characters.

### File-Level Acceptance Criteria

1. `CONTRIBUTING.md` no longer instructs users to copy `ask-eric/` to repo root unless the repo is actually restructured to support that.
2. `CONTRIBUTING.md` no longer claims `plugin.json` contains `"skills": "."` unless that field truly exists and is supported in this repo design.
3. `plugins/prism/skills/ask-eric/README.md` links to the correct `eric-engineering-mind.md` path or rewrites the sentence to avoid a broken relative link.
4. `plugins/prism/skills/ask-eric/README.md` contains valid UTF-8 readable text with no replacement-glyph corruption.
5. `CHANGELOG.md` includes the current released version shown in:
   - `.claude-plugin/marketplace.json`
   - `plugins/prism/.claude-plugin/plugin.json`
6. If `1.3.0` is not the intended release version, both manifest files must be changed down to the documented release version instead.
7. Root docs (`README.md`, `README.zh-TW.md`, `CLAUDE.md`, `CONTRIBUTING.md`) tell a consistent story about:
   - repo structure
   - extension path
   - validation status
8. Validation status for `ask-founder` is documented in a place users will actually read, not only in internal planning docs.

### Verification Commands

Run these before claiming completion:

```bash
rg -n '"skills": "\\."' CONTRIBUTING.md plugins/prism/.claude-plugin/plugin.json
rg -n 'ask-yourname|copy `ask-eric/`|auto-discovers' CONTRIBUTING.md
rg -n 'eric-engineering-mind\.md' README.md README.zh-TW.md plugins/prism/skills/ask-eric/README.md CLAUDE.md
rg -n '1\.3\.0|1\.2\.0|1\.1\.0|1\.0\.0' CHANGELOG.md .claude-plugin/marketplace.json plugins/prism/.claude-plugin/plugin.json
test -e eric-engineering-mind.md && echo "universal prompt exists"
```

Expected result:

1. No stale `"skills": "."` claim remains unless intentionally implemented.
2. No broken extension-path guidance remains.
3. All references to `eric-engineering-mind.md` are intentional and resolvable.
4. Version references are explainable and consistent.
5. The universal prompt file exists at repo root.

## Task 1: Fix the contributor extension path

**Files:**
- Modify: `CONTRIBUTING.md`
- Reference: `README.md`
- Reference: `CLAUDE.md`
- Reference: `plugins/prism/.claude-plugin/plugin.json`

**Step 1: Inspect the current contradiction**

Read:

```bash
sed -n '1,80p' CONTRIBUTING.md
sed -n '228,250p' README.md
sed -n '1,40p' CLAUDE.md
sed -n '1,40p' plugins/prism/.claude-plugin/plugin.json
```

Expected: `CONTRIBUTING.md` describes a root-level copy flow that does not match the actual `plugins/prism/skills/` structure.

**Step 2: Rewrite the contribution instructions**

Update `CONTRIBUTING.md` so the "Create Your Own Prism Instance" section reflects the actual repo structure. Choose one of these approaches and make the docs consistent:

1. Preferred: keep current repo structure and instruct contributors to copy `plugins/prism/skills/ask-eric/` to `plugins/prism/skills/ask-yourname/`.
2. Alternative: if you deliberately want root-level skill folders, restructure the repo and manifests first. Do not leave docs ahead of reality.

The rewrite must explicitly answer:

1. Where the new skill directory should live
2. Which files must be copied
3. How Claude Code discovers and invokes the new skill or command
4. Whether additional command wiring is required

**Step 3: Run doc consistency verification**

Run:

```bash
rg -n 'ask-yourname|copy `ask-eric/`|auto-discovers' CONTRIBUTING.md README.md CLAUDE.md
```

Expected: any remaining matches are accurate and consistent with the chosen repo structure.

**Step 4: Commit**

```bash
git add CONTRIBUTING.md
git commit -m "docs: fix prism extension path guidance"
```

## Task 2: Reconcile release versioning

**Files:**
- Modify: `CHANGELOG.md`
- Modify or confirm: `.claude-plugin/marketplace.json`
- Modify or confirm: `plugins/prism/.claude-plugin/plugin.json`

**Step 1: Determine the intended release truth**

Read:

```bash
sed -n '1,80p' CHANGELOG.md
sed -n '1,40p' .claude-plugin/marketplace.json
sed -n '1,40p' plugins/prism/.claude-plugin/plugin.json
```

Decide which is authoritative:

1. `1.3.0` is the intended current release and `CHANGELOG.md` is stale
2. `1.1.0` is the intended current release and both manifest files are ahead by mistake

Do not invent a version. Make the files tell one consistent truth.

**Step 2: Apply the minimum coherent fix**

If `1.3.0` is correct:

1. Add `1.3.0` and any missing `1.2.0` release notes to `CHANGELOG.md`
2. Ensure release notes explain the user-visible delta

If `1.1.0` is correct:

1. Change both manifest files to `1.1.0`
2. Re-read root docs for any now-stale references

**Step 3: Verify version alignment**

Run:

```bash
rg -n '1\.3\.0|1\.2\.0|1\.1\.0|1\.0\.0' CHANGELOG.md .claude-plugin/marketplace.json plugins/prism/.claude-plugin/plugin.json
```

Expected: the latest version in both manifest files is documented in `CHANGELOG.md`.

**Step 4: Commit**

```bash
git add CHANGELOG.md .claude-plugin/marketplace.json plugins/prism/.claude-plugin/plugin.json
git commit -m "docs: reconcile prism release versioning"
```

## Task 3: Repair the universal-prompt usage path

**Files:**
- Modify: `plugins/prism/skills/ask-eric/README.md`
- Reference: `README.md`
- Reference: `README.zh-TW.md`
- Reference: `eric-engineering-mind.md`

**Step 1: Confirm the current breakage**

Run:

```bash
sed -n '60,80p' plugins/prism/skills/ask-eric/README.md
test -e plugins/prism/skills/eric-engineering-mind.md; echo $?
test -e eric-engineering-mind.md; echo $?
```

Expected:

1. The current relative link in `plugins/prism/skills/ask-eric/README.md` does not resolve
2. The root file does exist
3. The text includes corrupted characters that should be cleaned up

**Step 2: Fix link and encoding issue**

Rewrite the non-Claude-Code section so it is both readable and correct. The simplest safe fix is:

1. Remove corrupted characters
2. Refer to the repo-root universal prompt clearly
3. If a relative link is awkward from this nested path, use plain text plus exact repo-relative path instead of a misleading markdown link

**Step 3: Verify readability**

Run:

```bash
sed -n '66,72p' plugins/prism/skills/ask-eric/README.md
rg -n 'eric-engineering-mind\.md' plugins/prism/skills/ask-eric/README.md
```

Expected: the sentence is readable UTF-8 text and does not imply a nonexistent path.

**Step 4: Commit**

```bash
git add plugins/prism/skills/ask-eric/README.md
git commit -m "docs: fix ask-eric universal prompt instructions"
```

## Task 4: Make validation claims honest and legible

**Files:**
- Modify: `README.md`
- Modify: `README.zh-TW.md`
- Modify: `CLAUDE.md`
- Optional create: `docs/superpowers/specs/2026-04-07-ask-founder-validation-status.md`
- Reference: `docs/superpowers/specs/2026-04-05-ask-eric-test-analysis-report.md`
- Reference: `docs/superpowers/specs/2026-04-06-founder-prism-design.md`

**Step 1: Inspect current claim surface**

Read:

```bash
sed -n '1,260p' README.md
sed -n '1,260p' README.zh-TW.md
sed -n '1,40p' CLAUDE.md
sed -n '1,80p' docs/superpowers/specs/2026-04-05-ask-eric-test-analysis-report.md
sed -n '1,80p' docs/superpowers/specs/2026-04-06-founder-prism-design.md
```

Expected: `ask-eric` has visible evaluation evidence, while `ask-founder` has design documentation but not equivalent test evidence.

**Step 2: Choose one honest messaging strategy**

Preferred option:

1. Keep both skills published
2. State clearly that `ask-eric` is the reference implementation with documented evaluation
3. State clearly that `ask-founder` is included and designed, but validation is currently lighter or pending equivalent eval documentation

Alternative option:

1. Produce equivalent validation documentation for `ask-founder`
2. Then update README claims to treat both skills as equally validated

Do not imply parity unless you can point to parity.

**Step 3: Update user-facing docs**

Update root docs so users can quickly answer:

1. Which skill is the reference implementation?
2. Which skill has published eval evidence?
3. What is the current maturity status of `ask-founder`?

If needed, add a short dedicated validation-status doc and link it from README.

**Step 4: Verify claim integrity**

Run:

```bash
rg -n 'reference implementation|validated|evaluation|ask-founder|ask-eric' README.md README.zh-TW.md CLAUDE.md docs/superpowers/specs
```

Expected: docs no longer imply unsupported equivalence between `ask-eric` and `ask-founder`.

**Step 5: Commit**

```bash
git add README.md README.zh-TW.md CLAUDE.md docs/superpowers/specs
git commit -m "docs: clarify prism validation status"
```

## Task 5: Final verification pass

**Files:**
- Verify all files touched above

**Step 1: Run the full verification bundle**

```bash
rg -n '"skills": "\\."' CONTRIBUTING.md plugins/prism/.claude-plugin/plugin.json
rg -n 'ask-yourname|copy `ask-eric/`|auto-discovers' CONTRIBUTING.md README.md CLAUDE.md
rg -n 'eric-engineering-mind\.md' README.md README.zh-TW.md plugins/prism/skills/ask-eric/README.md CLAUDE.md
rg -n '1\.3\.0|1\.2\.0|1\.1\.0|1\.0\.0' CHANGELOG.md .claude-plugin/marketplace.json plugins/prism/.claude-plugin/plugin.json
test -e eric-engineering-mind.md && echo "universal prompt exists"
git diff --stat
```

Expected:

1. No stale contributor guidance remains
2. No broken universal-prompt instruction remains
3. Versioning is coherent
4. Docs match repo structure
5. Diff only contains intentional remediation changes

**Step 2: Human review pass**

Manually read these files top-to-bottom once:

1. `README.md`
2. `README.zh-TW.md`
3. `CONTRIBUTING.md`
4. `CLAUDE.md`
5. `plugins/prism/skills/ask-eric/README.md`

Check for:

1. Contradictions
2. Broken narrative flow
3. Oversold claims
4. Encoding issues

**Step 3: Final commit**

```bash
git add README.md README.zh-TW.md CONTRIBUTING.md CLAUDE.md CHANGELOG.md .claude-plugin/marketplace.json plugins/prism/.claude-plugin/plugin.json plugins/prism/skills/ask-eric/README.md docs/superpowers/specs
git commit -m "docs: align prism docs metadata and validation claims"
```

## Definition of Done

This remediation is done only when all statements below are true:

1. A new contributor can follow `CONTRIBUTING.md` without guessing where custom skills belong.
2. A reader can compare plugin metadata and changelog and see one coherent release story.
3. A non-Claude-Code user can locate `eric-engineering-mind.md` from every documented entry point.
4. User-facing docs distinguish clearly between design completeness and validation completeness.
5. No review finding from the previous audit remains open in user-facing docs or metadata.
