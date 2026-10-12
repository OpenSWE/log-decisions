# log-decisions

An append-only `DECISIONS.md` journal recording the consequential calls the spec didn't settle — what was chosen, by whom, and why, with decide / assume / escalate rules for what an agent may settle alone.

**General-purpose.** The journal isn't coding-specific: any agent-assisted work — research, writing, ops, data — produces judgment calls someone will later ask *"why was it done this way?"* about. This skill gives those calls one durable, `grep`-able home at the project root.

It ships as an **[Agent Skill](https://agentskills.io)** — pure markdown, no scripts — so it runs on **Claude Code, Codex, Gemini CLI, Cursor**, and any other skills-compatible agent.

## Install

### Universal (any skills-compatible agent)

```text
npx skills add OpenSWE/log-decisions
```

### Claude Code (plugin)

```text
/plugin marketplace add OpenSWE/log-decisions
/plugin install log-decisions@log-decisions
```

## What it does

The skill ([`skills/log-decisions/SKILL.md`](skills/log-decisions/SKILL.md)) defines:

- **The bar** — a call is journal-worthy when it is *load-bearing*: later work, or the reader's acceptance of this work, rests on it, and the diff and commit message don't already carry it. Detail work chosen inside an existing pattern — a name, a value, a position — belongs in the commit message, not the journal.
- **The 2×2** — classify each call as *determinable × reversible*, then **decide** (grounded by an artifact), **assume** (safe default, logged for async review), or **escalate** (stop and ask). A catastrophic floor — data loss, irreversible spend, sending or publishing what can't be recalled, breaking something others depend on — always escalates.
- **The entry** — one append-only block per decision, written at the moment of the call: Question, Options considered, Chosen, Decided-by, Justification, Outcome, with `Supersedes:` for revisions. Never edited, never reordered.
- **The handoff** — when work is handed back, the `assumed` and `escalated` entries it appended are listed — what to confirm or revise, what's blocked — so the reader gets the review queue without opening the journal.

## Links

- **Discussion** — [Show HN thread](https://news.ycombinator.com/item?id=49264597)
- **Inspiration** — [Thariq's implementation-notes prompt](https://x.com/trq212/status/2056418157305454805), whose reader-facing framing, running-notes timing, and confirm-or-revise queue this skill absorbed in 1.1.0
- **Claude Code plugin** — install with the commands above; submitted to Anthropic's [Plugin Directory](https://code.claude.com/docs/en/discover-plugins) (pending review)

## Used by

[`swe-workflow`](https://github.com/swe-workflow/swe-workflow) — the idea → PRD → issues → ship suite — orchestrates this skill across every stage: spec-layer grills journal their assumed answers through it, and ship builds stage entries to a per-worktree `DECISIONS.staged.md` promoted at close-out. It was extracted from that repo (≤ v2.0.2) into this standalone one.

## License

MIT
