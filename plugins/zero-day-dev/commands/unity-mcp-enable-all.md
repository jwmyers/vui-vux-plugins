---
name: unity-mcp-enable-all
description: Enables all Unity MCP tool settings
allowed-tools: "*"
---

# Enable Unity MCP Tools

Set the Unity MCP tool configuration to maximum with all tools available.

## Purpose

Unity MCP tools can return large amounts of data, so normally we have them disabled or enabled in groups. This will turn on all possible tools

## Process

1. Review current AI-Game-Developer-Config.json settings

2. Apply absolute defaults:

   - leave all resources `true`
   - leave all prompts `false`
   - set all tools to `true`

3. Save updated configuration and notify the user.

## Configuration File

Location: `Assets/Resources/AI-Game-Developer-Config.json`
