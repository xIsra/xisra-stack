---
name: token-diet
description: Use when choosing a model tier, delegating to subagents, or watching token spend and usage.
---

# Token diet (3-level system)

Optimize **cost per solved task**, not price per token: a cheap model looping five times costs more than one clean pass at the right level. Scope: models doing agent work, not models your product calls.

## Levels

| Level | Task share | Use for | Score floor (% of CursorBench top) |
| --- | --- | --- | --- |
| **L1** | 80% | Scoped edits, tests, boilerplate, lookups, executing a plan | 70% |
| **L2** | 15% | Root-cause debugging, multi-file tracing, review, reversible migrations | 88% |
| **L3** | 5% | Architecture, ambiguous specs, irreversible or security calls | 97% |

Map each level to the model you can use with the lowest cost per task on [CursorBench](https://cursor.com/cursorbench) whose score clears its floor. Never hardcode model names. Remap weekly or when a model is unavailable; if CursorBench is unreachable, keep the last map and say so.

Shares count tasks, not dollars. They flag drift; they are not a quota, so never push a task down a level to hit them.

## Route

1. **Start at L1** when the goal, files, and done-check are known.
2. **L1 → L2** after 2 failed attempts at the same error, or when the cause spans 2+ files or services.
3. **L2 → L3** when viable designs differ in hard-to-reverse ways, the spec contradicts itself, or L2 fails twice.
4. **Drop to L1** once L3 writes the plan or L2 names the fix.
5. **Switch between steps**, never mid-step: the new model rereads context without cache. Hand over only the goal, verified facts, failing output, and file paths.
6. **A model or level the user asks for wins.** If you cannot switch your own model, apply levels to subagents you launch, or tell the user which level the next task needs.

```text
Flaky test, spec clear                  → L1 tries a fix
Same failure after 2 tries, 2 services  → L2 finds a race in queue.ts
L2 names the fix                        → L1 edits, given goal + failing output + file
```

## Watch spend

Check usage at session start and before any L3 run or batch job. If you cannot see usage, ask the user once; never guess.

- **Pacing:** budget % used minus % of billing cycle elapsed. Over 10 points means running hot.
- **Top spend:** which models, sessions, agents, and automations cost most.
- **Drift (weekly, 20+ tasks):** L2 + L3 above 20% of tasks, or cost per completed task or rework rate up over 25% from last week.
- **Leaks:** recurring automations, polling loops, retry storms, sessions with context over half full, and work left on L2/L3 after its plan or fix exists.

When running hot, move routine work to L1, pause recurring automations (or ask the user to), and get user confirmation before any L3 run or paid API call. If retries drive L1 spend, escalate after 1 failed attempt instead of 2. If rework rises for a task type, route it one level up.

## Trim context

- Read only the files and line ranges you need.
- Grep or tail logs; paste at most 50 relevant lines.
- Start a fresh session for each new task.
