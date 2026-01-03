---
description: Initialize structured planning workflow with agent/skill/command checklist
argument-hint: [task-description]
---

Initialize planning workflow for: $ARGUMENTS

## Step 1: Load Domain Knowledge

Invoke the `agent-coordination` skill for workflow patterns and agent guidance.

Based on the task, identify and invoke relevant domain skills:

| Domain | Skill | Invoke If Task Involves |
|--------|-------|-------------------------|
| Game rules | zero-day-rules | mechanics, phases, scoring, token movement |
| Architecture | project-architecture | code patterns, layers, namespaces, state flow |
| Input | board-sdk | touch, pieces, contacts, simulator, glyphs |
| Layout | layout-sizing | coordinates, positioning, screen dimensions, SVG |
| Visual | visual-style-guide | colors, rendering order, visual feedback |
| MCP | unity-mcp-tools | Unity Editor operations, scene hierarchy |
| Testing | unity-testing | EditMode/PlayMode tests, test coverage |
| Docs | documentation | updating documentation, CLAUDE.md |

## Step 2: Select Agents

Choose specialized agents based on task domain:

| Agent | Use When Task Involves |
|-------|------------------------|
| **code-architect** | ANY implementation plan (ALWAYS include for code changes) |
| game-designer | game rules, mechanics, player experience |
| ui-ux-developer | layout, sizing, visual feedback, coordinates |
| input-developer | Board SDK, touch input, piece detection, simulator |
| scene-builder | Unity hierarchy, GameObjects, prefabs, components |
| test-engineer | writing or running tests |
| deployment-specialist | building APK, deploying to Board hardware |
| mcp-advisor | MCP tool selection, connection troubleshooting |
| project-producer | documentation, workflow coordination |

## Step 3: Pre-Agent Setup

Before launching agents:

1. **Enable MCP tools if needed:**
   - For scene work: `/unity-mcp-enable scene-read gameobject`
   - For full Unity operations: `/unity-mcp-enable-all`
   - Check status: `/unity-mcp-status`

2. **Constraint reminder:** Only orchestrator can execute commands, not subagents.

## Step 4: Execute

1. Launch selected agents IN PARALLEL using a single message with multiple Task tool calls
2. Provide each agent with:
   - Specific focus area
   - Context from invoked skills
   - Relevant constraints

## Step 5: Synthesize Results

After agents complete:

1. Create attribution table:

   | Agent | Key Finding | Agent ID |
   |-------|-------------|----------|
   | [name] | [finding] | [id] |

2. Identify consensus and conflicts
3. Clarify with user if needed

## Step 6: Write Plan

Create plan file at `C:\Users\jon\.claude\plans\[plan-name].md` containing:
- Goal and requirements
- Agent review summary (attribution table)
- Implementation phases
- Files to modify
- Testing checklist

## Step 7: Cleanup

After planning work completes:
- Reset MCP tools if enabled: `/unity-mcp-reset`
- Note agent IDs for potential resumption
- Consider `/update-documentation` if learnings warrant capture

---

**Proceed with planning for:** $ARGUMENTS
