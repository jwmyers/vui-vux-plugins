# zero-day-dev Plugin

Comprehensive Unity game development assistant for Zero-Day Attack targeting Board hardware.

## Version

0.3.0

## Overview

This plugin provides specialized agents, skills, and commands for developing the Zero-Day Attack Unity game for Board hardware. It integrates with Unity MCP for direct Unity Editor interaction.

## Components

### Agents (9)

| Agent                     | Purpose                                           |
| ------------------------- | ------------------------------------------------- |
| **project-producer**      | Workflow orchestration, documentation maintenance |
| **game-designer**         | Game rules, mechanics, player experience          |
| **scene-builder**         | Unity scene hierarchy, GameObjects, prefabs       |
| **ui-ux-developer**       | Layout, sizing, visual feedback                   |
| **input-developer**       | Board SDK, touch input, piece detection           |
| **code-architect**        | Code structure, patterns, namespaces              |
| **test-engineer**         | Writing and running tests                         |
| **deployment-specialist** | Building APK, deploying to Board                  |
| **mcp-advisor**           | MCP tool advice, troubleshooting                  |

### Skills (9)

| Skill                    | Domain                                      |
| ------------------------ | ------------------------------------------- |
| **zero-day-rules**       | Game mechanics, phases, scoring             |
| **project-architecture** | Namespaces, singletons, layers              |
| **board-sdk**            | Touch input, pieces, contacts               |
| **layout-sizing**        | Screen dimensions, coordinates, SVG imports |
| **visual-style-guide**   | Colors, rendering order                     |
| **unity-mcp-tools**      | MCP tool usage and best practices           |
| **unity-testing**        | EditMode/PlayMode tests                     |
| **agent-coordination**   | Multi-agent workflows and orchestration     |
| **documentation**        | Doc conventions and maintenance             |

### Commands (11)

| Command                 | Description                            |
| ----------------------- | -------------------------------------- |
| `/start-planning`       | Orchestrated multi-agent task planning |
| `/build-apk`            | Build APK for Board hardware           |
| `/deploy-apk`           | Deploy to Board via bdb                |
| `/run-unity-test`       | Run Unity tests via MCP                |
| `/start-unity-mcp`      | Start MCP server                       |
| `/unity-mcp-reset`      | Reset MCP tools to disabled state      |
| `/unity-mcp-enable`     | Enable specific MCP tool groups        |
| `/unity-mcp-enable-all` | Enable all MCP tools at once           |
| `/unity-mcp-scene-info` | Query scene via MCP Resource           |
| `/unity-mcp-status`     | Show enabled MCP tool groups           |
| `/update-documentation` | Update project documentation           |

## Prerequisites

- Unity 6 with Board SDK
- Unity MCP configured and running
- Board Developer Bridge (bdb) for deployment

## Setup

1. Plugin components are in `agents/`, `commands/`, and `skills/` directories
2. Start MCP server: `start-mcp-server.bat`
3. Open Unity Editor
4. In Claude Code, run `/mcp` to verify connection

## Usage

### Starting Development

```text
/start-unity-mcp     # Start the MCP server
```

### Planning Complex Tasks

```text
/start-planning [task]  # Multi-agent orchestrated planning
```

### Building and Deploying

```text
/build-apk           # Build APK
/deploy-apk          # Deploy to Board
```

### Testing

```text
/run-unity-test             # Run EditMode tests
/run-unity-test PlayMode    # Run PlayMode tests
```

### Documentation

```text
/update-documentation       # Update docs after changes
```

### MCP Tool Management

```text
/unity-mcp-status     # Check which tools are enabled
/unity-mcp-enable scene-read gameobject  # Enable specific groups
/unity-mcp-enable-all # Enable all tools
/unity-mcp-reset      # Disable all tools
/unity-mcp-scene-info # Query scene (always available)
```

## Agent Triggering

Agents trigger automatically based on context:

- Discussing game rules → **game-designer**
- Creating GameObjects → **scene-builder**
- Working on layout → **ui-ux-developer**
- Implementing input → **input-developer**
- Planning architecture → **code-architect**
- Running tests → **test-engineer**
- Building/deploying → **deployment-specialist**
- MCP troubleshooting → **mcp-advisor**
- Workflow coordination → **project-producer**

## Directory Structure

```text
commands/                   # Slash commands
├── build-apk.md
├── deploy-apk.md
├── run-unity-test.md
├── start-planning.md
├── start-unity-mcp.md
├── unity-mcp-enable.md
├── unity-mcp-enable-all.md
├── unity-mcp-reset.md
├── unity-mcp-scene-info.md
├── unity-mcp-status.md
└── update-documentation.md

agents/                     # Specialized agents
├── code-architect.md
├── deployment-specialist.md
├── game-designer.md
├── input-developer.md
├── mcp-advisor.md
├── project-producer.md
├── scene-builder.md
├── test-engineer.md
└── ui-ux-developer.md

skills/                     # Domain knowledge
├── agent-coordination/
├── board-sdk/
├── documentation/
├── layout-sizing/
├── project-architecture/
├── unity-mcp-tools/
├── unity-testing/
├── visual-style-guide/
└── zero-day-rules/
```

## Architecture Notes

### Subagent Capabilities

**Subagents CAN:**

- Use MCP tools directly when tools are enabled in config
- Access skills declared in their `skills:` frontmatter field
- Use all standard Claude Code tools (Read, Edit, Bash, etc.)

**Subagents CANNOT:**

- Execute slash commands (only main orchestrator and user can)
- Enable/disable MCP tools themselves

### MCP Tool Workflow

1. **Main orchestrator** enables required tool groups via `/unity-mcp-enable [groups]`
2. **Main orchestrator** spawns subagent with appropriate skills
3. **Subagent** uses MCP tools directly to accomplish task
4. **Main orchestrator** runs `/unity-mcp-reset` when MCP work is complete

### MCP Resource (Always Available)

The MCP Resource "GameObject from Current Scene by Path" is always enabled and provides read-only scene inspection without requiring tool enablement. Use `/unity-mcp-scene-info {path}` to query.

### Tool Groups (11 total)

| Group       | Purpose                 |
| ----------- | ----------------------- |
| scene-read  | Inspect scene hierarchy |
| scene-write | Modify scenes           |
| gameobject  | GameObject operations   |
| component   | Component operations    |
| script      | Script operations       |
| prefab      | Prefab operations       |
| assets      | Asset management        |
| testing     | Run Unity tests         |
| editor      | Full editor control     |
| packages    | Package management      |
| reflection  | Advanced operations     |

See `skills/unity-mcp-tools/references/tool-groups.md` for complete tool definitions.
