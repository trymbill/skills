---
name: find-bugs
description: >
  Run a rigorous three-agent bug-finding pipeline on a codebase or file set.
  Triggers when the user runs `/find-bugs` or asks to find bugs, audit code for
  issues, do a thorough bug review, or hunt for vulnerabilities using a
  structured multi-agent approach. Use this skill any time the user wants a
  comprehensive, adversarial bug hunt — not just a quick review.
---

# Find Bugs — Three-Agent Pipeline

A structured adversarial bug-finding workflow adapted from @systematicls's method.
Three agents run in sequence, each with fresh context and a different mission:

1. **Hunter** — finds everything, scores by severity
2. **Skeptic** — challenges every finding, filters false positives
3. **Referee** — makes final calls on disputed bugs

---

## Workflow Overview

```
[Codebase/Input]
      │
      ▼
 Agent 1: Hunter        ← finds all potential bugs, scores them
      │
      │  (Hunter results passed in)
      ▼
 Agent 2: Skeptic       ← challenges and disproves as many as possible
      │
      │  (Both Hunter + Skeptic results passed in)
      ▼
 Agent 3: Referee       ← final arbiter, produces verified bug list
      │
      ▼
 [Verified Bug Report]
```

---

## How to Execute This Skill

Each agent must be run with a clean mental slate — no carryover assumptions from
previous agents. Follow these steps exactly:

### Step 1 — Scope the target

Before running agents, establish:
- What codebase / files / schema / data are being analyzed?
- Are there any areas to focus on (auth, DB, API layer, etc.)?
- What's the tech stack?

If the user hasn't specified, ask them now. Do not proceed until scope is clear.

### Step 2 — Run Agent 1: Hunter

Read the full agent prompt from: `references/hunter-agent.md`

Run the Hunter agent against the scoped codebase. Be exhaustive and aggressive —
false positives are OK, missing real bugs is not. Score every finding.

Produce a numbered list of all bugs found with scores. Label this section clearly:

```
═══════════════════════════════════════
  HUNTER AGENT RESULTS
═══════════════════════════════════════
```

### Step 3 — Run Agent 2: Skeptic

Read the full agent prompt from: `references/skeptic-agent.md`

**Reset your perspective entirely.** You are now a different agent whose goal is
to DISPROVE the Hunter's findings. Take the Hunter results from Step 2 and
challenge every single one. Apply the 2× penalty logic to decide what to dismiss.

Produce a full analysis. Label this section clearly:

```
═══════════════════════════════════════
  SKEPTIC AGENT RESULTS
═══════════════════════════════════════
```

### Step 4 — Run Agent 3: Referee

Read the full agent prompt from: `references/referee-agent.md`

**Reset again.** You are now a neutral arbiter. You have both the Hunter's findings
AND the Skeptic's challenges. Make final calls on each disputed bug. Your verdict
is final.

Produce the final verified bug list. Label this section clearly:

```
═══════════════════════════════════════
  REFEREE VERDICT — VERIFIED BUG LIST
═══════════════════════════════════════
```

### Step 5 — Final Summary

After the Referee section, produce a clean executive summary:

```
═══════════════════════════════════════
  FINAL REPORT
═══════════════════════════════════════
Total bugs found by Hunter: X
Bugs disproved by Skeptic: X
Bugs confirmed by Referee: X

CRITICAL bugs: X  🔴
MEDIUM bugs:   X  🟡
LOW bugs:      X  🟢

[Numbered list of confirmed bugs, severity, location]
```

---

## Tips for Best Results

- The more code/context you can provide, the more the Hunter can find
- If running on a large codebase, tell Claude which files/directories to focus on first
- You can re-run just the Skeptic or Referee if you want to re-challenge results
- For critical systems, consider running the Hunter twice from different angles

---

## Reference Files

- `references/hunter-agent.md` — Hunter agent system prompt
- `references/skeptic-agent.md` — Skeptic agent system prompt
- `references/referee-agent.md` — Referee agent system prompt
