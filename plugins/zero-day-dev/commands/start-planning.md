---
description: Enact structured planning workflow with agent/skill/command checklist
allowed-tools: "*"
model: inherit
argument-hint: [task-description]
---

# Planning and Execution Workflow Summary

Enact planning workflow for: $1

If there is no $1 request input from the user.

Update $1 according to user feedback and repeat steps as necessary before continuing to the next step.

Execute once the plan is approved, then cleanup

## Step 1: Load Domain Knowledge

Invoke the `agent-coordination` skill for workflow patterns and agent guidance.

Based on $1, identify and invoke relevant domain skills:

| Domain       | Skill                | Invoke If Task Involves                          |
| ------------ | -------------------- | ------------------------------------------------ |
| Game rules   | zero-day-rules       | mechanics, phases, scoring, token movement       |
| Architecture | project-architecture | code patterns, layers, namespaces, state flow    |
| Input        | board-sdk            | touch, pieces, contacts, simulator, glyphs       |
| Layout       | layout-sizing        | coordinates, positioning, screen dimensions, SVG |
| Visual       | visual-style-guide   | colors, rendering order, visual feedback         |
| MCP          | unity-mcp-tools      | Unity Editor operations, scene hierarchy         |
| Testing      | unity-testing        | EditMode/PlayMode tests, test coverage           |
| Docs         | documentation        | updating documentation, CLAUDE.md                |

## Step 2: Select Agents

Choose specialized agents based on $1 domain:

| Agent                 | Use When Task Involves                                     |
| --------------------- | ---------------------------------------------------------- |
| code-architect        | ANY implementation plan (USUALLY include for code changes) |
| game-designer         | game rules, mechanics, player experience                   |
| ui-ux-developer       | layout, sizing, visual feedback, coordinates               |
| input-developer       | Board SDK, touch input, piece detection, simulator         |
| scene-builder         | Unity hierarchy, GameObjects, prefabs, components          |
| test-engineer         | writing or running tests                                   |
| deployment-specialist | building APK, deploying to Board hardware                  |
| mcp-advisor           | MCP tool selection, connection troubleshooting             |
| project-producer      | documentation, workflow coordination                       |

## Step 3: Pre-Agent Setup

If the agent tasks and $1 require information about the Unity state or the execution of Unity work, load the `unity-mcp-tools` skill or spawn the `mcp-advisor` skill for guidance on this step.

Before launching agents, enable Unity MCP Tools based on the exploration and planning needs for $1:

1. **Enable or disable Unity MCP tools with commands as needed:**

   - Check Unity MCP Tools status with this command if needed: `unity-mcp-status`
   - Reset Unity MCP Tools with command if unneeded tools are enabled: `/unity-mcp-reset`
   - To enable needed Unity MCP Tool groups use this command: `/unity-mcp-enable [group1] [group2]`
   - For full Unity MCP Tools operations: `/unity-mcp-enable-all`

2. **Constraint reminder:** Only orchestrator can execute commands, not subagents.

## Step 4: Deploy Agents

1. Launch selected agents IN PARALLEL using a single message with multiple Task tool calls
2. Provide each agent with:
   - Specific focus area based on $1
   - Context from invoked skills
   - Unity MCP Tools enablement status
   - Relevant constraints

## Step 5: Synthesize Results

After agents complete:

1. Create attribution table:

   | Agent  | Key Finding | Agent ID |
   | ------ | ----------- | -------- |
   | [name] | [finding]   | [id]     |

2. Identify consensus and conflicts
3. Clarify with user if needed

## Step 6: Write Plan

Create plan file containing:

- Goal and requirements
- Agent review summary (attribution table)
- Implementation phases
- Files to modify
- Testing checklist

## Step 7: Execution

Upon plan approval, orchestrate subagents:

1. Write a ToDo with specific tasks for plan execution
2. Repeat Steps 1-3 with a focus on plan execution rather than planning
3. Deploy newly selected agents to execute, providing them with:
   - Specific focus and tasks to complete
   - Critical context from the approved plan
   - Context from invoked skills
   - Unity MCP Tools enablement status
   - Relevant constraints
4. Execute tasks until plan is complete

## Step 8: Cleanup and Summary

After plan execution is completes:

- Reset Unity MCP Tools command if enabled: `/unity-mcp-reset`
- Note agent IDs for potential resumption
- Consider `/update-documentation` commmand if learnings warrant capture
- Provide a summary to the user, including details on which agent accomplished which tasks

---

**Proceed with planning for:** $ARGUMENTS
