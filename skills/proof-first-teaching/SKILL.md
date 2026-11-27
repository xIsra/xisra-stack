---
name: proof-first-teaching
description: Use when creating, diagnosing, or planning educational content, tutorials, or a content niche.
---

# Proof-first teaching

The artifact (code, template, slides, steps) is available elsewhere. What earns attention is proof that it works and the reasoning behind each choice.

## Skip

- Entertainment or commentary with no teaching goal.
- Packaging only: titles, thumbnails, layout, SEO, formatting.
- Transcription or summary with no instructional design.
- Reach, growth, or algorithm tactics.

## Gather first

Get these from the author or the source before writing:

1. **Audience.** Who it is for and what they can already do. Assume they are skeptical, not that they are expert: trust comes from proof, not credentials.
2. **Problem.** The mistake, weak default, or gap this fixes.
3. **Proof.** What the author can show working: output, demo, before/after, a real case, a measured result.

Never invent proof, results, experience, or credentials. Write first-person experience only from what the author gave you. If something is missing, ask. If you must draft anyway, leave a marked placeholder such as `[your result]`.

```text
Given:   A salary negotiation email script. No outcomes.
Wrong:   "I used this script to land a 20% raise."
Right:   "This script got [your result] when [your situation]."
Ask:     "Have you sent this yourself? What happened?"
```

## Build

1. **Open with the problem and the promise.** Name the gap, then say what the audience will be able to do after, with a countable scope. Take a stand only if the piece proves it.
2. **Show the result.** Demonstrate it working before setup, bio, or background. Keep only warnings that prevent harm or data loss, placed where they apply.
3. **Teach in small units.** Each unit is one step the audience can finish, plus why it beats the obvious alternative and what breaks without it. Spend words on the details standard versions skip.
4. **Close on the promise.** End with the audience holding the outcome from step 1.

```text
Weak:   Here is my CI config template.
Strong: Most CI configs reinstall every dependency on each push. This one
        finishes in 40s instead of 6 min. Three lines do the work.

Weak:   My favorite pizza dough recipe.
Strong: Home-oven pizza comes out soggy because the base never gets hot
        enough. Two changes get a crisp base at 250°C, no stone needed.
```

One unit, with its reason and its failure:

```text
Step:   Key the cache on the lockfile hash, not the branch name.
Why:    The lockfile changes only when dependencies do; branches change
        on every pull request.
Breaks: Key on the branch and every new pull request starts cold.
```

Write as the practitioner: state choices and opinions, and address the audience as "you". Match depth to their level; beginners still get proof, with fewer assumed steps.

## Diagnose

Before polishing an existing or planned piece, ask: is the artifact all it offers? If yes, rebuild it around proof and reasoning. Polish will not fix it.

Either way, check it against Build. Report each failing step with the line that shows it, then fix in that order.

```text
Draft:  "Hi, I've designed for 12 years. Today: color theory.
         Download my palette below."
Gate:   Fails. The palette is all it offers. Rebuild, do not polish.
Step 1: "Today: color theory" names no problem and no outcome.
Step 2: The bio comes before any result.
Fix:    "Red/green status colors fail for about 1 in 12 men. Five swaps
         fix it, each with the reason." Then show it on a real screen.
```

## Choose a lane

Keep a topic or niche only if the author has evidence for all three:

1. **Need.** People are stuck on it and looking for help.
2. **Proof.** The author has real work or results to show.
3. **Depth.** Enough distinct problems for many pieces, and interest that will last.

Ease and trendiness do not count. Mark anything the author has not shown as unknown, ask for it, and do not assume it.

```text
Lane:    Spreadsheet automation for small accounting firms
Need:    Yes. The same bank-reconciliation questions recur in forums.
Proof:   Yes. The author built the reconciliation sheet their firm uses.
Depth:   Unknown. No topics named beyond reconciliation. Ask for ten.
Verdict: Hold until Depth is shown.
```

## After shipping

Find where the audience drops off or what they keep asking, using whatever signal the format has. Check that part against Build. The usual miss is no proof, no reason why, or no real problem up front.
