---
name: unity-mcp-reset
description: Reset Unity MCP tool settings to minimal defaults for context preservation
allowed-tools:
  - Read
  - Write
  - Edit
---

# Reset Unity MCP Settings

Reset the Unity MCP tool configuration to disable all tools, freeing context space after MCP work is complete.

## Purpose

After completing MCP operations (scene modifications, testing, etc.), use this command to disable tool groups and preserve context window space. The MCP Resource remains available for scene inspection.

## Usage

```
/unity-mcp-reset
```

## What Gets Reset

| Item             | Action                         |
| ---------------- | ------------------------------ |
| All tools (50)   | Set to `enabled: false`        |
| All prompts (47) | Unchanged (remain `false`)     |
| MCP Resource     | **Unchanged** (remains `true`) |

**Important**: The MCP Resource "GameObject from Current Scene by Path" is NOT affected by reset. It always remains enabled for scene inspection.

## Process

1. Read current AI-Game-Developer-Config.json settings
2. Set all tools to `enabled: false`
3. Leave resources and prompts unchanged
4. Save updated configuration
5. Report what was disabled

If all tools are already disabled, notify the user.

## Configuration File

Location: `Assets/Resources/AI-Game-Developer-Config.json`

## When to Use

- After scene-builder completes modifications
- After test-engineer runs tests
- After any MCP tool operation
- When mcp-coordinator suggests cleanup

## Output Format

```text
## MCP Tools Reset

### Disabled
- gameobject (8 tools)
- component (7 tools)
- testing (3 tools)

### Still Available
- MCP Resource: GameObject from Current Scene by Path (always enabled)
- Use `/unity-mcp-scene-info` for scene inspection

All tool groups disabled. Context preserved.
```

## Related Commands

- `/unity-mcp-enable [groups]` - Enable specific tool groups
- `/unity-mcp-status` - Check current enabled status
- `/unity-mcp-scene-info` - Query scene objects (always available)
