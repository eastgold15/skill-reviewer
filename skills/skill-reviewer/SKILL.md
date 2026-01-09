---
name: Skill Reviewer
description: This skill should be used when the user asks to "review skill execution", "analyze skill performance", "review agent trace", "analyze skill effectiveness", "analyze tool effectiveness", "optimize skill", "optimize tool", "review tool", or mentions evaluating execution quality across engineering correctness, goal achievement, and efficiency optimization.
version: 0.6.0
---

# Skill Reviewer

## Overview

A universal execution review tool that evaluates Skill/Tool/Agent execution performance through **three-layer progressive analysis**.

```
L1 Engineering Correctness ──▶ L2 Goal Achievement ──▶ L3 Optimization Space
   Is execution correct?         Is effect good?          Can it be better?
```

## When to Use

- Skill/Tool execution results don't meet expectations
- Agent behavior is abnormal and needs troubleshooting
- Want to systematically improve implementation

## Four Input Dimensions

```
Required                           Optional
┌─────────────┐                  ┌─────────────┐
│ 1. Execution │                  │ 3. Implementation │ ← Skill/Tool source
│    Trace     │                  │    Reference      │
│ 2. Execution │                  │ 4. Agent          │ ← Agent source
│    Goal      │                  │    Implementation │
└─────────────┘                  └─────────────┘
```

| Input | Description | Source |
|-------|------------|--------|
| Execution Trace | Tool calls, output, errors | User paste |
| Execution Goal | Original prompt | User provides |
| Implementation Reference | Skill/Tool definition or source | Auto-read |
| Agent Implementation | Agent source (optional) | User provides path |

> See `references/input-guide.md` for details

## Three-Layer Analysis

### L1: Engineering Correctness

**Question: Is execution correct?**

- Are tool calls successful?
- Do scripts execute without errors?
- Any Linter/syntax errors?
- Any infinite loops?

**Judgment:** If errors found → Report and stop, fix L1 first

### L2: Goal Achievement

**Question: Is the effect good?**

- Is the goal correctly understood?
- Are key steps executed?
- How is output format/quality?

**Rating:** ✓✓✓ Excellent / ✓✓ Good / ✓ Pass / ✗ Fail

### L3: Optimization Space

**Question: Can it be better?** (Prerequisite: L1 pass + L2 at least pass)

- Any redundant calls?
- Token usage efficiency?
- Can implementation be improved?

**Output:** Specific suggestions for Skill/Tool/Agent

> See `references/analysis-dimensions.md` for details

## Quick Workflow

```
Step 1: Collect inputs
        ↓
Step 2: Read implementation reference (if available)
        ↓
Step 3: L1 scan → Report if issues found
        ↓
Step 4: L2 comparison → Evaluate achievement
        ↓
Step 5: L3 optimization → Generate suggestions
        ↓
Step 6: Output report
```

**Guide user:**
```
Please provide:
1. [Required] Execution trace - Agent execution process
2. [Required] Execution goal - Your original prompt
3. [Optional] Analysis target - Skill name or Tool path
4. [Optional] Agent source path (for deep analysis)
```

> See `references/scenarios.md` for details

## Output Format

```markdown
## Execution Review Report

### Basic Information
| Item | Content |
|------|---------|
| Analysis Target | {Skill/Tool/Agent} |
| Execution Goal | "{prompt}" |

### L1: Engineering Correctness ✓/✗
[Check result table]

### L2: Goal Achievement ✓✓
[Achievement status + Rating]

### L3: Optimization Space 💡
[Optimization suggestions list]

### Summary
[Core issues + Priority improvements]
```

> See `references/report-templates.md` for complete template

## References

| Document | Content |
|----------|---------|
| `references/input-guide.md` | Detailed guide for four input dimensions |
| `references/analysis-dimensions.md` | Three-layer checklist |
| `references/scenarios.md` | Typical scenario guide |
| `references/report-templates.md` | Complete report templates |
