# OpenSWE skills

**[Agent Skills](https://agentskills.io)** from OpenSWE. Each one is pure markdown with no scripts, so it runs on **Claude Code, Codex, Gemini CLI, Cursor**, and any other skills-compatible agent.

| Skill | What it does |
|---|---|
| [`log-decisions`](#log-decisions) | An append-only `DECISIONS.md` journal of the consequential calls the spec didn't settle. |
| [`distill-prompt`](#distill-prompt) | Distills a conversation's goal into one prompt that reaches the same outcome in a fresh session. |

This repo was `OpenSWE/log-decisions` until 2026-10-14. GitHub redirects the old URL, so old clones and `npx skills add OpenSWE/log-decisions` still work.

## Install

### Universal (any skills-compatible agent)

```text
npx skills add OpenSWE/skills                        # every skill
npx skills add OpenSWE/skills --skill log-decisions  # one skill
```

### Claude Code (plugin)

Each skill is its own plugin in the `openswe` marketplace:

```text
/plugin marketplace add OpenSWE/skills
/plugin install log-decisions@openswe
/plugin install distill-prompt@openswe
```

On Claude Code 2.1.275 or later, one step does both: `/plugin install log-decisions --marketplace OpenSWE/skills`.

If you installed `log-decisions@log-decisions` before the rename, uninstall it and install `log-decisions@openswe`.

## log-decisions

An append-only `DECISIONS.md` journal recording the consequential calls the spec didn't settle — what was chosen, by whom, and why, with decide / assume / escalate rules for what an agent may settle alone.

**General-purpose.** The journal isn't coding-specific: any agent-assisted work — research, writing, ops, data — produces judgment calls someone will later ask *"why was it done this way?"* about. This skill gives those calls one durable, `grep`-able home at the project root.

The skill ([`skills/log-decisions/SKILL.md`](skills/log-decisions/SKILL.md)) defines:

- **The bar** — a call is journal-worthy when it is *load-bearing*: later work, or the reader's acceptance of this work, rests on it, and the diff and commit message don't already carry it. Detail work chosen inside an existing pattern — a name, a value, a position — belongs in the commit message, not the journal.
- **The 2×2** — classify each call as *determinable × reversible*, then **decide** (grounded by an artifact), **assume** (safe default, logged for async review), or **escalate** (stop and ask). A catastrophic floor — data loss, irreversible spend, sending or publishing what can't be recalled, breaking something others depend on — always escalates.
- **The entry** — one append-only block per decision, written at the moment of the call: Question, Options considered, Chosen, Decided-by, Justification, Outcome, with `Supersedes:` for revisions. Never edited, never reordered.
- **The handoff** — when work is handed back, the `assumed` and `escalated` entries it appended are listed — what to confirm or revise, what's blocked — so the reader gets the review queue without opening the journal.

Links:

- **Discussion** — [Show HN thread](https://news.ycombinator.com/item?id=49264597)
- **Inspiration** — [Thariq's implementation-notes prompt](https://x.com/trq212/status/2056418157305454805), whose reader-facing framing, running-notes timing, and confirm-or-revise queue this skill absorbed in 1.1.0
- **Claude Code plugin** — submitted to Anthropic's [Plugin Directory](https://code.claude.com/docs/en/discover-plugins) (pending review)

Used by [`swe-workflow`](https://github.com/swe-workflow/swe-workflow) — the idea → PRD → issues → ship suite — which orchestrates this skill across every stage: spec-layer grills journal their assumed answers through it, and ship builds stage entries to a per-worktree `DECISIONS.staged.md` promoted at close-out. It was extracted from that repo (≤ v2.0.2).

## distill-prompt

Run it at the end of a session with `/distill-prompt`. It reads the whole conversation and writes one prompt that a fresh session, with no memory of it, can run to reach the same final outcome.

The prompt states **what**, not how: the outcome as the user finally steered it, the taste they enforced through their corrections, and the facts a fresh session cannot discover by looking. The skill ([`skills/distill-prompt/SKILL.md`](skills/distill-prompt/SKILL.md)) runs only when you invoke it.

## License

MIT
