---
name: unity-mcp-enable
description: Enable specific Unity MCP tool groups by name
allowed-tools: "*"
---

# Enable MCP Tool Groups

Enable specific Unity MCP tool groups to allow scene modification, testing, or other operations.

## Usage

```text
/unity-mcp-enable [group1] [group2]
```

**Example command usage:**

- `/unity-mcp-enable gameobject component` - Enable GameObject and component operations
- `/unity-mcp-enable testing` - Enable test running
- `/unity-mcp-enable` - Show available groups

## Available Groups

| Group       | Tools Included                                                                                                                                                                               | Use Case                |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| scene-read  | scene-get-data, scene-list-opened,console-get-logs                                                                                                                                           | Inspect scene hierarchy |
| scene-write | scene-create, scene-save, scene-open, scene-set-active, scene-unload, console-get-logs                                                                                                       | Modify scenes           |
| gameobject  | gameobject-create, gameobject-find, gameobject-modify, gameobject-destroy, gameobject-duplicate, gameobject-set-parent, scene-save, console-get-logs                                         | GameObject operations   |
| component   | gameobject-component-add, gameobject-component-get, gameobject-component-modify, gameobject-component-destroy, component-list, scene-save, console-get-logs                                  | Component operations    |
| script      | script-read, script-update-or-create, script-delete, script-execute, assets-refresh, editor-application-get-state, console-get-logs                                                          | Script operations       |
| prefab      | assets-prefab-create, assets-prefab-instantiate, assets-prefab-open, assets-prefab-save, assets-prefab-close, assets-refresh, editor-application-get-state, console-get-logs                 | Prefab operations       |
| assets      | assets-find, assets-create-folder, assets-copy, assets-move, assets-delete, assets-get-data, assets-modify, assets-refresh, assets-material-create, assets-shader-list-all, console-get-logs | Asset management        |
| testing     | tests-run, editor-application-get-state, console-get-logs                                                                                                                                    | Run Unity tests         |
| editor      | editor-application-get-state, editor-application-set-state, console-get-logs, editor-selection-get, editor-selection-set                                                                     | Full editor control     |
| packages    | package-list, package-add, package-remove, package-search, console-get-logs                                                                                                                  | Package management      |
| reflection  | reflection-method-find, reflection-method-call, console-get-logs                                                                                                                             | Advanced operations     |

## Cross-cutting Utilities

These tools are automatically included when enabling related groups:

| Tool                         | Auto-included with      |
| ---------------------------- | ----------------------- |
| console-get-logs             | ALL groups              |
| editor-application-get-state | script, testing, prefab |
| assets-refresh               | script, prefab          |
| scene-save                   | gameobject, component   |

## Process

1. Parse requested group names from user input
2. If no groups specified, list available groups
3. Read `C:/Users/jon/Documents/GitHub/zero-day-attack/Assets/Resources/AI-Game-Developer-Config.json`
4. For each requested group:
   - Find all tools in that group
   - Include cross-cutting utilities
   - Set `enabled: true` for each tool
5. Save the updated config
6. Report which tools were enabled

## Configuration File

Location: `C:/Users/jon/Documents/GitHub/zero-day-attack/Assets/Resources/AI-Game-Developer-Config.json`

## Group Definitions

```json
{
  "scene-read": ["scene-get-data", "scene-list-opened", "console-get-logs"],
  "scene-write": [
    "scene-create",
    "scene-save",
    "scene-open",
    "scene-set-active",
    "scene-unload",
    "console-get-logs"
  ],
  "gameobject": [
    "gameobject-create",
    "gameobject-find",
    "gameobject-modify",
    "gameobject-destroy",
    "gameobject-duplicate",
    "gameobject-set-parent",
    "scene-save",
    "console-get-logs"
  ],
  "component": [
    "gameobject-component-add",
    "gameobject-component-get",
    "gameobject-component-modify",
    "gameobject-component-destroy",
    "component-list",
    "scene-save",
    "console-get-logs"
  ],
  "script": [
    "script-read",
    "script-update-or-create",
    "script-delete",
    "script-execute",
    "assets-refresh",
    "editor-application-get-state",
    "console-get-logs"
  ],
  "prefab": [
    "assets-prefab-create",
    "assets-prefab-instantiate",
    "assets-prefab-open",
    "assets-prefab-save",
    "assets-prefab-close",
    "assets-refresh",
    "editor-application-get-state",
    "console-get-logs"
  ],
  "assets": [
    "assets-find",
    "assets-create-folder",
    "assets-copy",
    "assets-move",
    "assets-delete",
    "assets-get-data",
    "assets-modify",
    "assets-refresh",
    "assets-material-create",
    "assets-shader-list-all",
    "console-get-logs"
  ],
  "testing": ["tests-run", "editor-application-get-state", "console-get-logs"],
  "editor": [
    "editor-application-get-state",
    "editor-application-set-state",
    "console-get-logs",
    "editor-selection-get",
    "editor-selection-set"
  ],
  "packages": [
    "package-list",
    "package-add",
    "package-remove",
    "package-search",
    "console-get-logs"
  ],
  "reflection": [
    "reflection-method-find",
    "reflection-method-call",
    "console-get-logs"
  ]
}
```

## Output Format

```text
## MCP Tool Groups Enabled

### Groups Enabled
- gameobject (8 tools)
- component (7 tools)

### Tools Now Active
- gameobject-create
- gameobject-find
- gameobject-modify
- gameobject-destroy
- gameobject-duplicate
- gameobject-set-parent
- gameobject-component-add
- gameobject-component-get
- gameobject-component-modify
- gameobject-component-destroy
- component-list
- scene-save
- console-get-logs

Ready for MCP operations.
```

## Notes

- MCP Resource "GameObject from Current Scene by Path" is always enabled (not affected)
- Use `/unity-mcp-reset` to disable all tools when done
- Use `/unity-mcp-status` to check currently enabled groups
