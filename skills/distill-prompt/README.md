# distill-prompt

Run it at the end of a session with `/distill-prompt`. It reads the whole conversation and writes one prompt that a fresh session, with no memory of it, can run to reach the same final outcome.

The prompt states **what**, not how: the outcome as the user finally steered it, the taste they enforced through their corrections, and the facts a fresh session cannot discover by looking. The skill ([`SKILL.md`](SKILL.md)) runs only when you invoke it.

## Install

```text
npx skills add OpenSWE/skills --skill distill-prompt
```

Claude Code plugin:

```text
/plugin marketplace add OpenSWE/skills
/plugin install skills@openswe   # all four OpenSWE skills
```

## License

MIT
