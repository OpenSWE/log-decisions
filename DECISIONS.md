<!-- AI-maintained, append-only -->

## 2026-08-11T14:42:55-07:00 — interactive/thariq-prompt — gate-resolution

**Question:** Which elements of Thariq's implementation-notes prompt should the skill absorb?
**Options considered:** adopt its three behaviors into the journal / also adopt its running-HTML-file format / add a separate per-task notes file alongside DECISIONS.md
**Chosen:** Absorb the three behaviors — reader-side significance test ("would the brief's author want to know before accepting?"), log-at-the-moment-of-the-call timing, and an at-handoff review queue of assumed/escalated entries — into the existing journal; the entry format is unchanged.
**Decided-by:** agent
**Justification:** The prompt's value is its framing (reader-facing, running, confirm-or-revise), not its format; a second notes file would split the single source of truth the journal exists to be, and an unchanged entry format keeps existing journals and the swe-workflow suite compatible.
**Outcome:** applied
**Ref:** (pending)

## 2026-08-11T14:43:10-07:00 — interactive/thariq-prompt — gate-resolution

**Question:** What vocabulary replaces the coding-specific terms when generalizing the skill?
**Options considered:** "brief" / "instructions" / "the ask" for the governing document; "project root" / "working directory" for the journal's location
**Chosen:** "brief" (defined once in the intro as instructions, requirements, a prompt, or an ask) and "project root"; the catastrophic floor and the worked example were rewritten domain-neutral (publishing/sending, a report-currency call).
**Decided-by:** agent (the generalization itself was directed by the user mid-session)
**Justification:** "Brief" is the domain-neutral term of art across writing, research, and consulting, and reads naturally for code too; "project root" names the same location without presuming version control.
**Outcome:** applied
**Ref:** (pending)

## 2026-08-11T14:46:24-07:00 — interactive/thariq-prompt — gate-resolution

**Question:** What vocabulary replaces the coding-specific terms when generalizing the skill?
**Options considered:** "brief" / "spec" / "instructions" for the governing document
**Chosen:** "spec", defined once in the intro as instructions, requirements, a prompt, or an ask; "project root" and the domain-neutral floor and example stand.
**Decided-by:** human
**Justification:** User chose the familiar term over "brief"; generality is carried by the inline definition rather than the word itself.
**Outcome:** applied
**Ref:** (pending)
**Supersedes:** 2026-08-11T14:43:10-07:00 — user reversed the agent's word choice

## Q4 — interactive/entry-format — deviation

**Question:** What identifier heads each journal entry?
**Options considered:** ISO-8601 timestamp (v1.1.0 format) / sequential question number (`Q1`, `Q12`, `Q13`)
**Chosen:** Sequential question numbers: `## Q<n> — <context> — <category>`, with `Supersedes:` citing the prior entry's Q-number; the date moves to version-control history.
**Decided-by:** human
**Justification:** User directed the change; Q-numbers are shorter to write and cite in `Supersedes:` lines and handoff summaries than timestamps, and the timing stays recoverable via blame.
**Outcome:** applied
**Ref:** (pending)
**Supersedes:** 2026-08-11T14:42:55-07:00 — only its "entry format is unchanged" clause; the absorbed behaviors stand

## Q5 — interactive/org-move — irreversible-action

**Question:** The skill is moving to the `OpenSWE` org. Transfer this repository, or publish a fresh copy there and archive this one?
**Options considered:** `gh` repo transfer / fresh repo in OpenSWE + archive here / leave it at `swe-workflow`
**Chosen:** Transfer. GitHub keeps the history, stars and issues, and serves a 301 from every `swe-workflow/log-decisions` URL, so existing clones, `npx skills add swe-workflow/log-decisions`, and the Show HN and Plugin Directory links keep resolving. Manifest `homepage`/`repository` and the README install commands were repointed at the new canonical URL and the version bumped to 1.2.1; `LICENSE`'s copyright holder was left as `swe-workflow`, since moving a repository between orgs does not transfer copyright.
**Decided-by:** human
**Justification:** A fresh copy would have dropped 4 stars and the issue history and, worse, pointed the *pending* Anthropic Plugin Directory review at an archived repo. The redirect makes the transfer the only option that is externally invisible. The user was told the review was pending against the old URL before approving.
**Outcome:** applied
**Ref:** `.claude-plugin/plugin.json`, `README.md`. Sibling move: `soulmachine/skills/herdr-advisor` → `OpenSWE/herdr-advisor`.

## Q6 — interactive/gate — deviation

**Question:** Why did the gate let a row-placement call through, and what replaces it?
**Options considered:** keep "when in doubt, log" and add non-examples / replace the doubt rule with a load-bearing test / drop the reader-side test entirely
**Chosen:** Replace "when in doubt, log" with a load-bearing test: an entry is owed when later work or the reader's acceptance rests on the call and the diff and commit message do not already carry it; detail work inside an existing pattern goes to the commit message. The doubt tie-break is now "draft the Question line; if the diff answers it, no entry". "Match the existing pattern" leaves the assume defaults, since a pattern makes a call determinable. Reader-side test stands.
**Decided-by:** human
**Justification:** A journal entry in a downstream repo recorded where a new row sits in a ranked table, placed by the table's own formula and a cited precedent commit — the user judged it not a decision. The old gate keyed on spec silence, which every detail satisfies, and "when in doubt, log" broke ties toward noise; the assume defaults listed pattern-matching as an assumption, inviting a determinable call to be logged as assumed.
**Outcome:** applied
**Ref:** (pending)

## Q7 — interactive/skills-repo — irreversible-action

**Question:** OpenSWE wants one repo for its published skills, starting with this one and `distill-prompt` from `soulmachine/skills`. Make a new `OpenSWE/skills`, or rename this repo to it?
**Options considered:** rename `OpenSWE/log-decisions` to `OpenSWE/skills` / new repo, archive this one / new repo, delete this one
**Chosen:** Rename, then copy `distill-prompt` in as `skills/distill-prompt/`. `plugin.json` is gone. `marketplace.json` is now the `openswe` marketplace with one plugin per skill, each `"source": "./"`, `"strict": false` and `"skills": ["./skills/<name>"]`. log-decisions stays at 1.3.1; distill-prompt starts at 1.0.0.
**Decided-by:** human (rename); agent (marketplace name and manifest shape)
**Justification:** The same reason as Q5: a rename keeps history, stars and issues, and GitHub redirects every old URL, so `npx skills add OpenSWE/log-decisions`, the Show HN link and the pending Plugin Directory review keep resolving. A marketplace named `log-decisions` would be wrong for a multi-skill repo, so it is now `openswe`. Users who installed `log-decisions@log-decisions` must reinstall; the README says how. One plugin per skill keeps each installable alone.
**Outcome:** applied
**Ref:** `.claude-plugin/marketplace.json`, `README.md`, `skills/distill-prompt/`. Source of the copy: `soulmachine/skills` 051f2ab.
