# AI Code Review Gates

**A 12-point slop filter, a pre-merge checklist and a code-reviewer subagent for AI-written code.**

AI coding agents write code fast, and they make the same mistakes over and over: invented APIs, swallowed errors, tests that assert nothing, "refactors" that quietly change behavior. These three files catch them before they reach your main branch. They work with any coding agent, or with no agent at all.

| File | What it is |
|---|---|
| [`gates/slop-filter.md`](gates/slop-filter.md) | The 12 mistakes AI agents make most often: how to spot each one and what to do about it |
| [`gates/pre-merge-checklist.md`](gates/pre-merge-checklist.md) | What a person signs off on before anything merges |
| [`.claude/agents/code-reviewer.md`](.claude/agents/code-reviewer.md) | A read-only Claude Code subagent that reviews a diff against both lists and reports findings by severity, with file, line and fix |
| [`.github/pull_request_template.md`](.github/pull_request_template.md) | The checklist as a pull request template, so authors tick it before asking for review |

## Quick start (2 minutes)

Copy the folders into the root of your repository:

```bash
git clone --depth 1 https://github.com/lean-team-products/ai-code-review-gates /tmp/gates
cp -r /tmp/gates/gates /tmp/gates/.claude /tmp/gates/.github your-repo/
```

Already have a `.github/pull_request_template.md` or `.claude/agents/`? Copy only the files you need.

**With Claude Code:** finish a change, then ask *"review my changes"*. Claude Code delegates to the `code-reviewer` subagent, which reads the diff and every changed file in full, runs your lint and tests, and returns:

```
VERDICT: CHANGES REQUIRED
Scope: 6 files reviewed (212 lines). Skipped: none

Blocking
1. src/billing/invoice.ts:88 — total is computed with floats
   Why it matters: rounding errors on every invoice over $1,000
   Fix: use integer cents (amountCents) end to end
...
Evidence
- npm test -- billing → 41 passed, 0 failed
```

It never edits code and never claims a test run it didn't do.

**With Cursor, Copilot or another agent:** add `gates/slop-filter.md` to your rules or instructions file and ask the agent to check its own diff against it before handing it over.

**Without AI:** use the slop filter as a review checklist and the PR template as your merge gate.

## The one-question test

Before merging, ask: **"Would I be comfortable defending this diff in review if I had written every line myself?"** If not, it isn't ready, no matter who or what wrote it.

## Want the rest?

These files are from the **[Lean Team Agent Kit](https://www.leanteamproducts.com/#manuals)**. The full kit adds:

- 9 more subagents: planner, test writer, debugger, security reviewer, refactorer, docs writer, dependency auditor, ops investigator and release manager
- 9 end-to-end skills: ship a feature, review a PR, triage an incident, run a database migration, cut a release and more
- a parallel-agents playbook and a 24-page manual

There's also a free **[Codebase Antipattern Checklist](https://www.leanteamproducts.com/?checklist=1)**: 48 signs a codebase is getting harder to change, as a PDF.

More practical notes on AI coding agents, logging costs and test suites are on the **[Lean Team blog](https://www.leanteamproducts.com/blog)**.

## License

MIT. Use these files however you like, including in commercial and internal projects.
