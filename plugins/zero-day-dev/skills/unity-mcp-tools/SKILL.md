---
name: Unity MCP Tools Usage
description: This skill should be used when the user asks about "MCP tool", "gameobject-", "script-", "scene-", "tests-run", "which tool should I use", "Unity MCP", "MCP server", "ai-game-developer", "create GameObject", "modify component", "run tests via MCP", or discusses using Unity MCP tools effectively.
version: 0.1.0
---

# Unity MCP Tools Usage

Expert knowledge of Unity MCP tools for interacting with the Unity Editor via Claude Code, including tool selection, best practices, and common patterns.

## MCP Overview

Unity MCP enables Claude Code to directly interact with Unity Editor:
- Query and modify scene hierarchy
- Create and modify GameObjects and Components
- Read, write, and execute C# scripts
- Run tests and get console logs
- Manage assets and prefabs

## Tool Categories

### Scene Operations

| Tool | Purpose | When to Use |
|------|---------|-------------|
| `scene-get-data` | Query scene hierarchy | Inspect current scene structure |
| `scene-create` | Create new scene | Starting fresh scene |
| `scene-save` | Save current scene | After modifications |
| `scene-open` | Open scene file | Switch to different scene |
| `scene-list-opened` | List open scenes | Check what's loaded |

### GameObject Operations

| Tool | Purpose | When to Use |
|------|---------|-------------|
| `gameobject-create` | Create new GameObject | Adding objects to scene |
| `gameobject-find` | Find GameObject by path/name | Locating existing objects |
| `gameobject-modify` | Modify GameObject properties | Changing name, active state |
| `gameobject-destroy` | Delete GameObject | Removing objects |
| `gameobject-duplicate` | Clone GameObject | Copying objects |
| `gameobject-set-parent` | Change hierarchy | Reorganizing scene |

### Component Operations

| Tool | Purpose | When to Use |
|------|---------|-------------|
| `gameobject-component-add` | Add component to GameObject | Adding behaviors |
| `gameobject-component-get` | Inspect component data | Reading component values |
| `gameobject-component-modify` | Change component values | Updating settings |
| `gameobject-component-destroy` | Remove component | Cleaning up |

### Script Operations

| Tool | Purpose | When to Use |
|------|---------|-------------|
| `script-read` | Read C# file contents | Inspecting code |
| `script-update-or-create` | Write/modify C# file | Creating or editing scripts |
| `script-delete` | Delete script file | Removing scripts |
| `script-execute` | Run arbitrary C# code | One-time operations |

### Asset Operations

| Tool | Purpose | When to Use |
|------|---------|-------------|
| `assets-find` | Search for assets | Locating files |
| `assets-create-folder` | Create folder | Organizing project |
| `assets-copy` | Copy asset | Duplicating files |
| `assets-move` | Move/rename asset | Reorganizing |
| `assets-delete` | Delete asset | Cleanup |
| `assets-get-data` | Get asset details | Inspecting assets |
| `assets-modify` | Modify asset | Updating asset properties |

### Prefab Operations

| Tool | Purpose | When to Use |
|------|---------|-------------|
| `assets-prefab-create` | Create prefab from GameObject | Saving reusable objects |
| `assets-prefab-instantiate` | Spawn prefab instance | Adding prefab to scene |
| `assets-prefab-open` | Enter prefab edit mode | Modifying prefab |
| `assets-prefab-save` | Save prefab changes | After editing |
| `assets-prefab-close` | Exit prefab edit mode | Done editing |

### Testing

| Tool | Purpose | When to Use |
|------|---------|-------------|
| `tests-run` | Execute Unity tests | Running EditMode/PlayMode tests |

### Editor Control

| Tool | Purpose | When to Use |
|------|---------|-------------|
| `editor-application-get-state` | Check editor state | Verify play mode, compilation |
| `editor-application-set-state` | Control editor | Start/stop play mode |
| `console-get-logs` | Get console output | Debugging, checking errors |

## Common Patterns

### Inspecting Scene Structure

```
1. Use scene-get-data to get hierarchy
2. Use gameobject-find for specific objects
3. Use gameobject-component-get to inspect components
```

### Creating New Object with Component

```
1. gameobject-create - Create the GameObject
2. gameobject-component-add - Add required components
3. gameobject-component-modify - Configure component values
```

### Modifying Existing Script

```
1. script-read - Read current contents
2. script-update-or-create - Write modified code
3. (Automatic) Compilation feedback provided
```

### Running Tests After Changes

```
1. Make code changes with script-update-or-create
2. tests-run with testMode: "EditMode" for fast tests
3. Check results and fix any failures
```

## Tool Selection Guide

### For Creating Things

| Want to Create | Use Tool |
|---------------|----------|
| New GameObject | `gameobject-create` |
| New C# script | `script-update-or-create` |
| New prefab | `gameobject-create` then `assets-prefab-create` |
| New folder | `assets-create-folder` |
| New scene | `scene-create` |

### For Finding Things

| Want to Find | Use Tool |
|-------------|----------|
| GameObject in scene | `gameobject-find` |
| Asset in project | `assets-find` |
| Component data | `gameobject-component-get` |
| Script contents | `script-read` |

### For Modifying Things

| Want to Modify | Use Tool |
|---------------|----------|
| GameObject properties | `gameobject-modify` |
| Component values | `gameobject-component-modify` |
| Script code | `script-update-or-create` |
| Asset properties | `assets-modify` |

## Best Practices

### Use Specific References

Prefer `instanceID` or `path` over `name` for reliable object finding:
```json
{
  "gameObjectRef": {
    "instanceID": 12345,
    "path": "TileManager/Tiles/Tile_2_2"
  }
}
```

### Batch Operations

When modifying multiple objects, use array parameters where supported to reduce round trips.

### Check Compilation

After `script-update-or-create`, the tool provides compilation feedback. Always check for errors before proceeding.

### Minimal Tool Calls

Prefer fewer, well-targeted tool calls over many exploratory ones:
- Use `scene-get-data` with appropriate depth
- Use `gameobject-component-get` with `includeFields: true` when needed

### Test After Changes

Run `tests-run` after significant code changes:
```json
{
  "testMode": "EditMode",
  "includePassingTests": false,
  "includeMessages": true
}
```

## MCP Connection

### Starting the Server

Run before opening Unity:
```bash
start-mcp-server.bat
```

### Verifying Connection

In Claude Code, run `/mcp` to verify green checkmark for `ai-game-developer`.

### Configuration

MCP configured in `.mcp.json` with HTTP mode for multi-session support.

## Component Type Names

When adding components, use full type names:

| Common Component | Full Name |
|-----------------|-----------|
| Transform | `UnityEngine.Transform` |
| SpriteRenderer | `UnityEngine.SpriteRenderer` |
| BoxCollider2D | `UnityEngine.BoxCollider2D` |
| Rigidbody2D | `UnityEngine.Rigidbody2D` |
| Custom Script | `ZeroDayAttack.View.TileView` |

## Reflection Tools

For advanced operations:

| Tool | Purpose |
|------|---------|
| `reflection-method-find` | Find methods by name |
| `reflection-method-call` | Call any method (including private) |

Use cautiously - prefer standard tools when possible.

## Additional Resources

### Reference Files

For complete MCP documentation:
- **Documentation/Unity-MCP-Documentation.md** - Full MCP guide
- **.mcp.json** - Connection configuration

### Component Search

Use `component-list` to find available component types by name.
