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

## Q8 — interactive/skills-repo — irreversible-action

**Question:** Frank asked to fold `OpenSWE/herdr-advisor` and `OpenSWE/lessons` into this repo. How do their history, journals and READMEs fit a repo that now holds four skills, and what happens to the old repos?
**Options considered:** merge with history / copy the files only; journal and README at the root / in each skill's folder; archive the old repos / delete them
**Chosen:** Merged each repo with `--allow-unrelated-histories`, so `git log` on a skill file still shows its full history. Each skill keeps its README in its own folder, and the root README is an index plus the install commands. herdr-advisor's journal is now `skills/herdr-advisor/DECISIONS.md`, and its SKILL.md and ADVISOR.md link there; this root journal stays the repo's and log-decisions' own. `THIRD-PARTY-NOTICES` moved into `skills/lessons/`. `marketplace.json` gained a plugin for each, at their old versions. The old repos get a pointer at the top of their README and are archived, not deleted.
**Decided-by:** human (fold); agent (layout, archive over delete)
**Justification:** Two Q-numbered journals cannot merge into one file without renumbering, which breaks every citation, so each skill's journal stays whole beside it. A journal in the skill folder ships with `npx skills add`, but nothing loads it into context. Archiving keeps existing installs working; deleting them would break them for no gain.
**Outcome:** applied
**Ref:** merge commits c3a68f6 (herdr-advisor) and 208c104 (lessons)

## Q9 — interactive/plugin-directory — deviation

**Question:** The Plugin Directory submission for log-decisions (portal id ecbfe5d1, since Aug 11) reads the plugin from the repo root of `swe-workflow/log-decisions`. Since Q7 the root has no `plugin.json`, and the portal cannot change a submission's repo or path. Pin it to an old tag, or withdraw it and submit again from a plugin folder?
**Options considered:** pin the tracked tag to 96cda54 / withdraw and resubmit with a new plugin folder
**Chosen:** Resubmit. Each plugin skill's folder is now its own plugin root: `skills/<name>/.claude-plugin/plugin.json` with `"skills": ["./"]`, and `marketplace.json` entries are `"source": "./skills/<name>"` instead of `strict: false`. Version, author, keywords and the rest now live in each `plugin.json`, so bump a version there. The new submission's path is `skills/log-decisions` in `OpenSWE/skills`.
**Decided-by:** human (resubmit); agent (plugin-root-in-skill-folder layout)
**Justification:** This layout leaves `skills/<name>/SKILL.md` where `npx skills` and the fleet's `agent-sync adopt` expect it, so nothing outside this repo changes. A plugin install now copies only the skill's own folder instead of the whole repo. Tested: `claude plugin validate --strict` passes for each plugin and the marketplace, a throwaway install shows exactly one skill per plugin, and `npx skills add -l` lists all four skills. herdr-advisor has no `plugin.json` (Q66 in its journal).
**Outcome:** applied
**Ref:** `.claude-plugin/marketplace.json`, `skills/*/.claude-plugin/plugin.json`

## Q10 — interactive/plugin-directory — deviation

**Question:** Frank wants the whole repo to be one Claude Code plugin holding all four skills, named `skills`, with the OpenSWE logo as its icon, submitted to the Plugin Directory in place of the old log-decisions submission. What does the layout become?
**Options considered:** one plugin at the repo root / one plugin per skill (Q9)
**Chosen:** The repo root is the plugin: `.claude-plugin/plugin.json` named `skills`, 1.0.0, with the four skills found by the default `skills/` scan, and `.claude-plugin/icon.png` copied from `coding-agent/products/openswe/logo.png` (1254 px square). `marketplace.json` lists that one plugin with `"source": "./"`. The per-skill `plugin.json` files from Q9 are gone. Install: `/plugin install skills@openswe`. The directory submission's path is the repository root of `OpenSWE/skills`.
**Decided-by:** human
**Justification:** One listing for all of OpenSWE's skills. The directory takes an icon only on the first submission, so the icon goes in before submitting. Tested: `claude plugin validate --strict` passes for the plugin and the marketplace, and a throwaway install shows 4 skills.
**Outcome:** applied
**Ref:** `.claude-plugin/`, README install sections; herdr-advisor Q67 makes that skill work from the plugin's folder
**Supersedes:** Q9 — one plugin instead of one per skill; Q7 — only its manifest shape

## Q11 — interactive/plugin-directory — irreversible-action

**Question:** With the repo now one plugin (Q10), replace the old log-decisions Plugin Directory submission (portal id ecbfe5d1, in review since Aug 11) with a new one?
**Options considered:** withdraw and resubmit / pin the old submission to a pre-Q7 tag
**Chosen:** Withdrew ecbfe5d1 and submitted `OpenSWE/skills`, repo root, `main` @ ea0a197, as plugin `skills` v1.0.0: portal id c846fe22-388e-4bb9-bb15-bab0c1d09074, contact zhiqushi@gmail.com. Data handling: no personal data, no data sent to other services, nothing retained, not for under-18s. All four compliance statements were ticked on Frank's instruction. The form's defaults were kept: auto-publish on, GitHub push webhook (not yet set up, so the 6-hourly check applies).
**Decided-by:** human
**Justification:** The old submission tracked a repo-root plugin that no longer exists. Validation passed with four policy holds that go to a reviewer: a credential finding (herdr-advisor's `$PWD` beside a docs URL), a journal entry naming the icon file, and the name "skills" resembling the listing "AI Skills". A `displayName` in plugin.json could clear the name hold later.
**Outcome:** applied
**Ref:** https://claude.ai/directory/manage/plugins/c846fe22-388e-4bb9-bb15-bab0c1d09074
