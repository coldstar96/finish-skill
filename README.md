# finish

A [Claude Code](https://claude.com/claude-code) skill that runs a goal to completion without
check-ins. It asks one batch of clarifying questions up front (goal, verifiable "done when"
criteria, scope, allowed outward actions), records them as a contract in `SUMMARY.md`, then works
unattended: ambiguity is decided and logged, failures are retried with a new approach, and anything
outside the contract is marked `BLOCKED` and skipped. It stops only when every criterion is verified
or only `BLOCKED` items remain, then reports PASS/BLOCKED with evidence.

Existing guardrails (CLAUDE.md rules, permission hooks) still apply; the skill removes questions,
not safety checks.

## Install

```bash
git clone https://github.com/coldstar96/finish-skill ~/.claude/skills/finish
```

Then ask Claude to "keep going until it's done" or type `/finish`.

## License

MIT
