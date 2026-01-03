---
name: unity-mcp-scene-info
description: Query Unity scene objects using the MCP Resource (always available, no tool enablement needed)
allowed-tools:
  - ReadMcpResourceTool
  - ListMcpResourcesTool
---

# Get Scene Object Information

Query detailed information about GameObjects in the Unity scene using the MCP Resource. This works without enabling any MCP tools.

## Usage

```text
/unity-mcp-scene-info [path]
```

**Examples:**

- `/unity-mcp-scene-info GameplayScene/TileManager`
- `/unity-mcp-scene-info GameplayScene/Tokens/RedAttack`
- `/unity-mcp-scene-info` (lists available resources)

## How It Works

Uses the MCP Resource "GameObject from Current Scene by Path" which is **always enabled**.

### Access Method

Use `ReadMcpResourceTool`:

- Server: `ai-game-developer`
- URI: `unity://gameobject/{scene}/{path}`

### Example Query

For path `GameplayScene/TileManager`:

```json
{
  "server": "ai-game-developer",
  "uri": "unity://gameobject/GameplayScene/TileManager"
}
```

## What It Returns

- **Transform**: position, rotation, scale
- **Components**: all attached component types
- **Properties**: component field values
- **Children**: child GameObject names and paths

## When to Use

| Scenario                       | Use This Command       |
| ------------------------------ | ---------------------- |
| Inspect scene structure        | Yes                    |
| Read component values          | Yes                    |
| Debug positioning issues       | Yes                    |
| Verify changes after MCP tools | Yes                    |
| Create/modify GameObjects      | No - use scene-builder |
| Add components                 | No - use scene-builder |

## Advantages

- **Always available**: No tool enablement required
- **No context cost**: Doesn't add MCP tools to context
- **Read-only**: Safe to use anytime
- **Detailed data**: Full component and property information

## Process

1. Parse the requested path from user input
2. Use `ReadMcpResourceTool` with:
   - Server: `ai-game-developer`
   - URI: `unity://gameobject/{scene}/{path}`
3. Parse and display the returned JSON data
4. Format component and property information clearly

## Output Format

```text
## GameObject: TileManager

### Transform
- Position: (0, 0, 0)
- Rotation: (0, 0, 0)
- Scale: (1, 1, 1)

### Components
- TileManager (ZeroDayAttack.View.TileManager)
- Transform (UnityEngine.Transform)

### Properties (TileManager)
- tileDatabase: TileDatabase (Asset)
- tilePrefab: GameObject (Prefab)

### Children (5)
- Tiles
- Grid
- ...
```

## Notes

- If no path provided, list available MCP resources
- The MCP Resource must be enabled in AI-Game-Developer-Config.json (should always be true)
- Works even when all MCP tools are disabled
