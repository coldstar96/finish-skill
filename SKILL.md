---
name: finish
description: Use when the user wants a goal finished autonomously without check-ins or questions - "keep going until it's done", "don't ask me anything", "run to completion", "work on this unattended", "I'll be away", "/finish".
---

# Finish

Clarify once at the start, then work until the goal is done. No questions after the clarification step.

## 1. Clarify (the only time you ask)

Before doing any work, ask the user once, in a single batch (e.g. `AskUserQuestion` in Claude Code, otherwise one message), to pin down:
- **Goal**: one sentence.
- **Done when**: numbered criteria you can verify yourself (test passes, build green, log line, file exists).
- **Scope**: what is in and what is off limits.
- **Allowed outward actions**: push, PR, comment, message, ticket. Anything not listed is not allowed.

Write the answers to a `SUMMARY.md` (in your session or scratch directory) as the contract. The user's answer is the go-ahead for every "show me first" or "wait for me" checkpoint within that scope.

## 2. Execute (no questions)

Loop until every "done when" item is verified:
- **Ambiguity**: pick the most reasonable option, log it under `Decisions` in `SUMMARY.md`, keep going.
- **Failure**: diagnose and try another approach. A failed attempt is not a reason to stop.
- **Waiting on async work**: use a background watcher, monitor or timer, and never end the turn idle.
- **Needs something outside the contract** (a guardrail or prohibited action, or info only the user has): skip that piece, note it as `BLOCKED`, carry on with everything else.

Do not end your turn with a question, a menu of options, or "should I continue?".

## 3. Stop

Stop only when all criteria are verified, or only `BLOCKED` items remain. Final message: each criterion PASS/BLOCKED with evidence, then the `Decisions` list.

Hard guardrails (project instruction files such as CLAUDE.md, permission hooks, security policy) still apply. This skill removes questions, not guardrails.
