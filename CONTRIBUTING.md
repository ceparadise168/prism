# Contributing to Prism

## Ways to Contribute

### 1. Create Your Own Prism Instance

The most valuable contribution is showing that the framework works for different people. Fork the repo, build your own, and share it.

**Steps:**

1. Fork this repo
2. Copy `ask-eric/` to `ask-yourname/`
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

**You don't need all 19 perspectives.** Start with the 5-7 that matter most to you. A focused Prism with 7 deep perspectives is better than 19 shallow ones.

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

## Code of Conduct

Be constructive. The whole point of Prism is multi-perspective thinking — disagreement is expected and valuable when it's about ideas, not people.
