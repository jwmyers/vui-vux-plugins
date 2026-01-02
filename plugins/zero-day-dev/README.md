# zero-day-dev Plugin

Comprehensive Unity game development assistant for Zero-Day Attack targeting Board hardware.

## Overview

This plugin provides specialized agents, skills, and commands for developing the Zero-Day Attack Unity game for Board hardware. It integrates with Unity MCP for direct Unity Editor interaction.

## Components

### Agents (8)

| Agent | Purpose |
|-------|---------|
| **project-producer** | Workflow orchestration, documentation maintenance |
| **game-designer** | Game rules, mechanics, player experience |
| **scene-builder** | Unity scene hierarchy, GameObjects, prefabs |
| **ui-ux-developer** | Layout, sizing, visual feedback |
| **input-developer** | Board SDK, touch input, piece detection |
| **code-architect** | Code structure, patterns, namespaces |
| **test-engineer** | Writing and running tests |
| **deployment-specialist** | Building APK, deploying to Board |

### Skills (8)

| Skill | Domain |
|-------|--------|
| **zero-day-rules** | Game mechanics, phases, scoring |
| **project-architecture** | Namespaces, singletons, layers |
| **board-sdk** | Touch input, pieces, contacts |
| **layout-sizing** | Screen dimensions, coordinates, SVG imports |
| **visual-style-guide** | Colors, rendering order |
| **unity-mcp-tools** | MCP tool usage and best practices |
| **unity-testing** | EditMode/PlayMode tests |
| **documentation** | Doc conventions and maintenance |

### Commands (6)

| Command | Description |
|---------|-------------|
| `/build` | Build APK for Board hardware |
| `/deploy` | Deploy to Board via bdb |
| `/test` | Run Unity tests via MCP |
| `/start-unity-mcp` | Start MCP server |
| `/unity-mcp-reset` | Reset MCP settings to minimal |
| `/document` | Update project documentation |

### Hooks (2)

- **PostToolUse** on `script-update-or-create`: Check compilation status
- **PreToolUse** on Write/Edit `.cs` files: Validate namespace conventions

## Prerequisites

- Unity 6 with Board SDK
- Unity MCP configured and running
- Board Developer Bridge (bdb) for deployment

## Setup

1. The plugin is already installed in this project at `.claude-plugin/`
2. Start MCP server: `start-mcp-server.bat`
3. Open Unity Editor
4. In Claude Code, run `/mcp` to verify connection

## Usage

### Starting Development

```
/start-unity-mcp     # Start the MCP server
```

### Building and Deploying

```
/build               # Build APK
/deploy              # Deploy to Board
```

### Testing

```
/test                # Run EditMode tests
/test PlayMode       # Run PlayMode tests
```

### Documentation

```
/document            # Update docs after changes
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
- Workflow coordination → **project-producer**

## Directory Structure

```
.claude-plugin/
├── plugin.json          # Plugin manifest
└── README.md            # This file

commands/                # Slash commands
├── build.md
├── deploy.md
├── test.md
├── start-unity-mcp.md
├── unity-mcp-reset.md
└── document.md

agents/                  # Specialized agents
├── project-producer.md
├── game-designer.md
├── scene-builder.md
├── ui-ux-developer.md
├── input-developer.md
├── code-architect.md
├── test-engineer.md
└── deployment-specialist.md

skills/                  # Domain knowledge
├── zero-day-rules/
├── project-architecture/
├── board-sdk/
├── layout-sizing/
├── visual-style-guide/
├── unity-mcp-tools/
├── unity-testing/
└── documentation/

hooks/
└── hooks.json           # Event hooks
```

## Version

0.1.0
