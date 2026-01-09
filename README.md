# Skill Reviewer

> [中文文档](README_CN.md) | English

![Skill Reviewer](./assets/skill-reviewer.png)

A universal execution review tool that evaluates Skill/Tool/Agent execution performance through three-layer progressive analysis.

## What is This?

**Skill Reviewer** is an AI-native tool designed to systematically analyze and improve the execution quality of AI Skills, Tools, and Agents. It provides a structured framework to:

- **Diagnose** execution issues quickly
- **Evaluate** whether goals are achieved
- **Optimize** efficiency and implementation

Think of it as a code review system, but for AI execution traces.

## Three-Layer Analysis Framework

```
L1 Engineering Correctness ──▶ L2 Goal Achievement ──▶ L3 Optimization Space
   Is execution correct?         Is effect good?          Can it be better?
```

- **L1 (Engineering)**: Catches technical errors - syntax errors, failed calls, infinite loops
- **L2 (Goal)**: Evaluates effectiveness - is the task actually completed well?
- **L3 (Optimization)**: Identifies improvements - redundant calls, token efficiency, better approaches

## Features

- ✅ **Universal**: Works with any Skill, Tool, or Agent
- 📊 **Systematic**: Three-layer progressive analysis
- 🎯 **Actionable**: Provides specific, prioritized improvement suggestions
- 🔍 **Comprehensive**: Four input dimensions for thorough analysis

## Installation

### Prerequisites

- An AI editor that supports MCP Skills (Claude Code, Cursor, Windsurf, etc.)
- Access to filesystem (for symlinking)

### Install via Symlink

```bash
# Clone the repository
git clone https://github.com/your-org/skill-reviewer.git
cd skill-reviewer

# Create symlink to your skills directory
ln -s $(pwd)/skills/skill-reviewer ~/.claude/skills/skill-reviewer
```

### Verify Installation

After installation, the skill should appear in your AI editor's skill list. You can verify by asking your AI assistant:

```
"List available skills"
```

## Usage Guide

### In Claude Code

1. **Trigger the skill** by asking:
  ```
   "Review this skill execution"
   "Analyze this agent trace"
   "Check if this tool works correctly"
  ```
2. **Provide required inputs** when prompted:
  - Execution trace (paste your agent logs)
  - Original goal (what you wanted to achieve)
3. **Optionally provide** for deeper analysis:
  - Skill/Tool name or file path
  - Agent source code path
4. **Receive structured report** with:
  - Engineering issues (if any)
  - Goal achievement rating
  - Optimization suggestions

**Example conversation:**

```
You: Review this skill execution

Claude: I'll help review the execution. Please provide:
1. [Required] Execution trace - The agent execution process
2. [Required] Execution goal - Your original prompt
3. [Optional] Which skill/tool was used?

You: [Paste execution trace]
     Goal: "Generate API documentation"
     Used: doc-generator skill

Claude: [Generates detailed review report]
```

### In Cursor

1. **Open Cursor** and ensure the skill is installed (symlinked to `~/.claude/skills/`)
2. **In chat or composer**, use natural language:
  ```
   "Review the execution of this agent task"
   "Analyze this skill performance"
  ```
3. **Provide context** by:
  - Pasting execution logs directly in chat
  - Referencing files with `@filename`
  - Sharing terminal output
4. **Get instant feedback** with actionable suggestions

**Tips for Cursor:**

- Use `@skill-reviewer` to explicitly invoke the skill
- Attach files with execution traces using drag-and-drop
- Reference specific code sections for targeted analysis

### In Windsurf

1. **Ensure skill is symlinked** to `~/.claude/skills/skill-reviewer`
2. **In cascade mode**, simply describe your need:
  ```
   "This agent execution didn't work as expected, help review it"
  ```
3. **Windsurf will automatically**:
  - Load the skill-reviewer
  - Guide you through input collection
  - Generate comprehensive report
4. **Use flow mode** for interactive review:
  - Ask questions about specific execution steps
  - Dive deeper into L1/L2/L3 layers
  - Iterate on optimization suggestions

### In Other MCP-Compatible Editors

If your editor supports MCP Skills:

1. **Install skill** via symlink to your editor's skills directory
2. **Trigger** by mentioning keywords: "review", "analyze", "skill execution"
3. **Follow prompts** to provide execution trace and goal
4. **Review output** and apply suggestions

## What to Provide for Review

### Required Inputs


| Input               | Description                              | How to Get                      |
| ------------------- | ---------------------------------------- | ------------------------------- |
| **Execution Trace** | Complete agent/tool execution log        | Copy from terminal/chat history |
| **Execution Goal**  | Original user prompt or task description | Your initial request            |


### Optional Inputs (for deeper analysis)


| Input                        | Description                        | When to Provide                   |
| ---------------------------- | ---------------------------------- | --------------------------------- |
| **Implementation Reference** | Skill/Tool source code or SKILL.md | When reviewing custom skills      |
| **Agent Implementation**     | Agent source code                  | When investigating agent behavior |


### Example Execution Trace

```
User: Generate API docs
↓
Agent: Reading openapi.yaml
Agent: Calling tool: parse_openapi(file="openapi.yaml")
Tool Output: [parsed structure]
Agent: Calling tool: generate_markdown(...)
Tool Output: docs/api.md created
Result: ✓ Documentation generated
```

## Output Example

After analysis, you'll receive a structured report:

```markdown
## Execution Review Report

### Basic Information
| Item | Content |
|------|---------|
| Analysis Target | doc-generator skill |
| Execution Goal | "Generate API documentation" |

### L1: Engineering Correctness ✓
✓ All tool calls successful
✓ No syntax errors
✓ Files created correctly

### L2: Goal Achievement ✓✓✓
✓✓✓ Excellent
- Documentation generated with correct structure
- All API endpoints covered
- Examples included

### L3: Optimization Space 💡
1. **Token Efficiency**: File read twice unnecessarily
2. **Implementation**: Could cache parsed OpenAPI structure
3. **Output**: Consider adding table of contents

### Summary
Execution successful with excellent results.
Priority optimization: Implement caching to reduce redundant file reads.
```

## Project Structure

```
skill-reviewer/
├── skills/
│   └── skill-reviewer/          # Main skill
│       ├── SKILL.md             # Skill definition
│       └── references/
│           ├── input-guide.md          # Input collection guide
│           ├── analysis-dimensions.md  # Analysis checklists
│           ├── scenarios.md            # Usage scenarios
│           └── report-templates.md     # Report formats
├── discuss/                      # Design documents
├── AGENTS.md                     # Skill development guide
├── README.md                     # This file
└── README_CN.md                  # Chinese documentation
```

## Documentation

- **[SKILL.md](skills/skill-reviewer/SKILL.md)** - Complete skill specification
- **[input-guide.md](skills/skill-reviewer/references/input-guide.md)** - Four input dimensions explained
- **[analysis-dimensions.md](skills/skill-reviewer/references/analysis-dimensions.md)** - L1/L2/L3 checklists
- **[scenarios.md](skills/skill-reviewer/references/scenarios.md)** - Common usage scenarios
- **[report-templates.md](skills/skill-reviewer/references/report-templates.md)** - Output formats

## Contributing

We welcome contributions! Please see [AGENTS.md](AGENTS.md) for:

- Skill development standards
- Design principles
- SKILL.md requirements
- Best practices

## Use Cases

### 1. Debugging Failed Executions

```
Scenario: Agent task failed, unsure why
Action: Provide execution trace → Get L1 engineering analysis
Result: Identify specific error and fix
```

### 2. Improving Performance

```
Scenario: Task works but feels slow
Action: Request full L1-L3 review
Result: Discover redundant calls, optimize token usage
```

### 3. Validating Custom Skills

```
Scenario: Built a new skill, want to verify quality
Action: Run test execution → Review with skill-reviewer
Result: Catch implementation issues before production
```

### 4. Learning Best Practices

```
Scenario: New to skill development
Action: Review example executions with L3 analysis
Result: Learn optimization patterns and anti-patterns
```

## FAQ

**Q: Do I need to provide all four inputs?**
A: No. Only execution trace and goal are required. Others enhance analysis depth.

**Q: Can it review human-written code?**
A: It's designed for AI execution traces, but principles apply to code review too.

**Q: How long does a review take?**
A: Typically 1-2 minutes for complete L1-L3 analysis.

**Q: Does it work with any Skill/Tool?**
A: Yes! It's implementation-agnostic and works with any execution trace.

**Q: Can I customize the analysis dimensions?**
A: The three layers are standard, but you can fork and modify for specific needs.

## License

MIT License - See LICENSE file for details

---

**Built for AI-native development** 🚀