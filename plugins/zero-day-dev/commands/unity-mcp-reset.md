---
name: unity-mcp-reset
description: Reset Unity MCP tool settings to minimal defaults for context preservation
allowed-tools:
  - Read
  - Write
  - Edit
---

# Reset Unity MCP Settings

Reset the Unity MCP tool configuration to minimal defaults to preserve context window space.

## Purpose

Unity MCP tools can return large amounts of data. This command configures default settings that minimize context usage while maintaining functionality.

## Process

1. Review current AI-Game-Developer-Config.json settings

2. Apply minimal defaults:
   - Reduce serialization depth
   - Limit hierarchy depth
   - Disable verbose output by default
   - Minimize included data fields

3. Save updated configuration

## Configuration File

Location: `Assets/Resources/AI-Game-Developer-Config.json`

## Minimal Settings Recommendations

When using MCP tools, prefer these patterns:

**Scene queries:**
```json
{
  "includeChildrenDepth": 1,
  "includeData": false,
  "deepSerialization": false
}
```

**Component inspection:**
```json
{
  "includeFields": true,
  "includeProperties": false,
  "deepSerialization": false
}
```

**Test runs:**
```json
{
  "includePassingTests": false,
  "includeMessages": true,
  "includeStacktrace": false,
  "includeLogs": false
}
```

## Best Practices

- Only request data actually needed
- Use shallow serialization unless deep inspection required
- Filter test output to failures only
- Limit hierarchy depth for scene queries

## Notes

This command helps maintain efficient context usage when working with Unity MCP tools. Adjust settings based on specific needs when deeper inspection is required.
