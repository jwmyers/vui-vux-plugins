---
name: unity-mcp-status
description: Show currently enabled Unity MCP tool groups and resource status
allowed-tools: "*"
---

# MCP Status

Show the current status of Unity MCP tools, including which tool groups are enabled and resource availability.

## Usage

```text
/unity-mcp-status
```

## Process

1. Read `Assets/Resources/AI-Game-Developer-Config.json`
2. Count enabled tools per group
3. Check resource status
4. Display summary

## Configuration File

Location: `Assets/Resources/AI-Game-Developer-Config.json`

## Group Definitions

Map tools to groups to determine which groups are "enabled":

| Group       | Tools                                                                                                                                                                      |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| scene-read  | scene-get-data, scene-list-opened                                                                                                                                          |
| scene-write | scene-create, scene-save, scene-open, scene-set-active, scene-unload                                                                                                       |
| gameobject  | gameobject-create, gameobject-find, gameobject-modify, gameobject-destroy, gameobject-duplicate, gameobject-set-parent                                                     |
| component   | gameobject-component-add, gameobject-component-get, gameobject-component-modify, gameobject-component-destroy, component-list                                              |
| script      | script-read, script-update-or-create, script-delete, script-execute                                                                                                        |
| prefab      | assets-prefab-create, assets-prefab-instantiate, assets-prefab-open, assets-prefab-save, assets-prefab-close                                                               |
| assets      | assets-find, assets-create-folder, assets-copy, assets-move, assets-delete, assets-get-data, assets-modify, assets-refresh, assets-material-create, assets-shader-list-all |
| testing     | tests-run                                                                                                                                                                  |
| editor      | editor-application-get-state, editor-application-set-state, editor-selection-get, editor-selection-set                                                                     |
| packages    | package-list, package-add, package-remove, package-search                                                                                                                  |
| reflection  | reflection-method-find, reflection-method-call                                                                                                                             |

A group is considered "enabled" if **any** of its core tools are enabled.

## Output Format

### When tools are enabled

```text
## MCP Status

### Resource (Always Available)
- GameObject from Current Scene by Path: ENABLED

### Enabled Groups
- gameobject (6/6 tools)
- component (5/5 tools)

### Enabled Tools (13 total)
- console-get-logs
- scene-save
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

### Disabled Groups
- scene-read, scene-write, script, prefab, assets, testing, editor, packages, reflection
```

### When no tools are enabled

```text
## MCP Status

### Resource (Always Available)
- GameObject from Current Scene by Path: ENABLED

### Tools
All tool groups disabled (default state)

### Available Groups
Use `/unity-mcp-enable [group]` to enable:
- scene-read, scene-write, gameobject, component, script, prefab, assets, testing, editor, packages, reflection
```

## Notes

- MCP Resource should always show as ENABLED
- If Resource shows DISABLED, this is an error state - it should always be enabled
- Use `/unity-mcp-enable` to enable specific groups
- Use `/unity-mcp-reset` to disable all tools
- Use `/unity-mcp-enable-all` to enable all tools
