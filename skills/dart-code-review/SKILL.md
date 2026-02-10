---
name: dart-code-review
description: Code review checklist for LLMs reviewing PRs and MRs. Use when reviewing pull requests, examining code changes, or when the user asks for a code review.
---

# Dart Code Review

## Overview

Checklist for LLM-driven code reviews of pull requests and merge requests. Covers branch hygiene, per-file verification, PR-level checks, and constructive feedback.

## Reference Files

See detailed documentation for each topic:

- [pre-review.md](references/pre-review.md) - Branch type, up-to-date, file list, connected components
- [review-mindset.md](references/review-mindset.md) - Objectivity, no assumptions, devil's advocate
- [per-file.md](references/per-file.md) - Directory, naming, logic, security, docs, tests
- [pr-level.md](references/pr-level.md) - Scope, description, tests, CI
- [feedback.md](references/feedback.md) - Constructive feedback, output format

## Quick Checklist

### Pre-Review
- [ ] Branch is feature/bugfix (not main/develop)
- [ ] Up-to-date with target
- [ ] List changed files
- [ ] Inspect connected components

### Per File
- [ ] Correct directory, naming, responsibility
- [ ] Readable, correct logic, modular
- [ ] Errors handled, no security/performance issues
- [ ] Documented, tested, matches style
- [ ] Generated files up-to-date

### PR-Level
- [ ] Focused change set
- [ ] Description matches changes
- [ ] Tests cover new/changed logic
- [ ] Tests assert real behavior
- [ ] CI passes

### Output
Conclusions and recommendations per file. Be objective; provide constructive feedback.
