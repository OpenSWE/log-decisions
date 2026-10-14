# OpenSWE skills

**[Agent Skills](https://agentskills.io)** from OpenSWE. They run on **Claude Code, Codex, Gemini CLI, Cursor**, and any other skills-compatible agent.

| Skill | What it does |
|---|---|
| [`log-decisions`](skills/log-decisions/) | An append-only `DECISIONS.md` journal of the consequential calls the spec didn't settle. |
| [`herdr-advisor`](skills/herdr-advisor/) | Pairs a [Herdr](https://github.com/herdrdev/herdr) worker with a stronger advisor model that unblocks it and leads it to its next task. |
| [`lessons`](skills/lessons/) | A `LESSONS.md` ledger: reviews merged work, records each lesson with evidence, and promotes repeated lessons into the code standards. |
| [`distill-prompt`](skills/distill-prompt/) | Distills a conversation's goal into one prompt that reaches the same outcome in a fresh session. |

Each skill's folder has its own README with details and requirements.

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
```

On Claude Code 2.1.275 or later, one step does both: `/plugin install log-decisions --marketplace OpenSWE/skills`.

## Where the skills came from

All three old repos were merged in on 2026-10-14, with their full commit history.

- This repo was `OpenSWE/log-decisions`. GitHub redirects that URL here, so old clones and `npx skills add OpenSWE/log-decisions` still work.
- `OpenSWE/herdr-advisor` and `OpenSWE/lessons` are archived. They still install, but they no longer get updates.
- If you installed a plugin as `<name>@<name>` (for example `log-decisions@log-decisions`), uninstall it and install `<name>@openswe`.

## License

MIT. Each skill folder may carry its own notices, such as [`skills/lessons/THIRD-PARTY-NOTICES`](skills/lessons/THIRD-PARTY-NOTICES).
