# Typical Analysis Scenarios Guide

## Scenario Overview

| Scenario | Input Combination | Analysis Depth | Typical Use Case |
|---------|------------------|----------------|------------------|
| A | Trace + Goal | L1 Basic | Quick troubleshooting of obvious errors |
| B | + Skill | L1-L3 | Analyze Skill execution effectiveness |
| C | + Tool | L1-L3 | Analyze Tool call effectiveness |
| D | + Agent | L1-L3 Deep | Analyze custom Agent |

---

## Scenario A: Quick Troubleshooting

**Input:** Execution trace + Execution goal

**Applicable:**
- Don't know what Skill was used
- Just want to quickly check for obvious errors
- Initial problem direction identification

**Analysis Capability:**
```
✓ L1 Engineering correctness check
  - Tool call errors
  - Script execution failures
  - Loop detection

△ L2 Goal achievement (limited)
  - Can only compare goal with final output
  - Cannot check step coverage

✗ L3 Optimization suggestions
  - Missing implementation reference, cannot give specific suggestions
```

**Workflow:**
```
1. Scan trace for error keywords
   grep: "error", "failed", "denied", "not found"

2. Detect loops
   Count consecutive identical tool calls

3. Compare goal with output
   Goal requirements vs actual output

4. Output L1 results + preliminary L2 judgment
```

---

## Scenario B: Skill Analysis

**Input:** Execution trace + Execution goal + Skill implementation

**Applicable:**
- Used specific Skill but effect not good
- Want to optimize Skill implementation
- Verify Skill design is correctly executed

**Analysis Capability:**
```
✓ L1 Engineering correctness check
✓ L2 Goal achievement
  - Step coverage check
  - Output format comparison
  - Quality assessment
✓ L3 Optimization suggestions
  - For SKILL.md
  - For scripts/
  - For references/
```

**Workflow:**
```
Step 1: Read Skill implementation
        cat skills/${SKILL_NAME}/SKILL.md
        ls skills/${SKILL_NAME}/

Step 2: Extract design elements
        - Workflow steps
        - Expected output format
        - Key scripts

Step 3: L1 check
        Scan errors, detect loops

Step 4: L2 comparison
        Design steps vs actual execution
        Mark: ✓ executed / ✗ skipped / △ partial

Step 5: L3 suggestions
        Propose improvements for deviation points
```

**L3 Suggestion Categories:**
```
For SKILL.md:
├── Step description unclear → Improve description
├── Key step skipped → Add emphasis markers
└── Output examples missing → Add examples/

For scripts/:
├── Script has bug → Fix
├── Error handling insufficient → Enhance
└── Efficiency issues → Optimize

For references/:
├── Documentation missing → Add
└── Examples outdated → Update
```

---

## Scenario C: Tool Analysis

**Input:** Execution trace + Execution goal + Tool implementation

**Applicable:**
- A Tool call effect not good
- Want to optimize Tool parameter design
- Tool return value doesn't meet expectation

**Analysis Capability:**
```
✓ L1 Engineering correctness check
✓ L2 Goal achievement
  - Are parameters used correctly
  - Are return values handled correctly
  - Does it meet Tool design intent
✓ L3 Optimization suggestions
  - Parameter definition optimization
  - Return format improvement
  - Description improvement
```

**Workflow:**
```
Step 1: Read Tool implementation
        cat path/to/tool/implementation.ts
        # Or extract definition from tools.json

Step 2: Extract Tool design
        - Parameter schema
        - Description
        - Processing logic
        - Return format

Step 3: L1 check
        - Is call successful
        - Are parameters valid

Step 4: L2 comparison
        - Does parameter use match design
        - Are return values correctly understood
        - Does it achieve expected effect

Step 5: L3 suggestions
        - Parameter design improvement
        - Description optimization
        - Error handling enhancement
```

**L3 Suggestion Categories:**
```
For Tool definition:
├── Description unclear → Improve description
├── Parameter design unreasonable → Optimize schema
└── Return format messy → Standardize

For Tool implementation:
├── Error handling insufficient → Add boundary checks
├── Return information insufficient → Enrich return content
└── Performance issues → Optimize logic
```

---

## Scenario D: Agent Deep Analysis

**Input:** Execution trace + Execution goal + Skill + Agent implementation

**Applicable:**
- Analyzing your own developed Agent
- Agent behavior doesn't match expectation
- Want to optimize Agent decision logic

**Analysis Capability:**
```
✓ L1 Engineering correctness check
✓ L2 Goal achievement
  - Skill step coverage
  - Is Agent decision reasonable
✓ L3 Deep optimization suggestions
  - Skill improvement
  - Tool improvement
  - System prompt improvement
  - Agent logic improvement
```

**Workflow:**
```
Step 1: Read all implementations
        # Skill
        cat skills/${SKILL_NAME}/SKILL.md
        
        # Agent
        cat ${AGENT_PATH}/system-prompt.md
        cat ${AGENT_PATH}/tools/*.ts

Step 2: Establish relationships
        Skill instruction → Agent understanding → Tool call

Step 3: L1 check
        Full-chain error check

Step 4: L2 comparison
        - Skill design vs Agent execution
        - Agent decision vs Tool call
        - Tool result vs final output

Step 5: L3 deep suggestions
        Locate which layer has the problem
```

**Problem Location Layers:**
```
Problem may be at:
├── Skill layer
│   └── Instruction unclear, Agent misunderstood
│
├── Agent layer
│   ├── System prompt missing constraints
│   ├── Tool definition description inaccurate
│   └── Decision logic has issues
│
└── Tool layer
    └── Implementation has bug, return value abnormal
```

---

## Scenario Selection Guide

```
Start
  │
  ├─ Just want to quickly check for errors?
  │     └─ Scenario A (Minimal)
  │
  ├─ Know what Skill was used?
  │     └─ Scenario B (Skill Analysis)
  │
  ├─ Mainly a Tool problem?
  │     └─ Scenario C (Tool Analysis)
  │
  └─ Analyzing your own Agent + have source?
        └─ Scenario D (Deep Analysis)
```
