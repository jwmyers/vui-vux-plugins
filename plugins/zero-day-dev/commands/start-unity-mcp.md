---
name: start-unity-mcp
description: Start the Unity MCP server before opening Unity
allowed-tools: "*"
---

# Start Unity MCP Server

Start the Unity MCP server using the project's startup script. The server must be running before Unity can connect.

## Process

1. Check if server is already running (port 56688)

2. Start the MCP server:

   ```bash
   start-mcp-server.bat
   ```

3. Confirm server is running

## User Startup Order (Critical)

```text
1. Run start-mcp-server.bat    ← This command
2. Open Unity Editor           ← Plugin auto-connects
3. Run /mcp to verify          ← Check connection
```

## Architecture

```text
┌─────────────┐                 ┌──────────────────┐              ┌──────────────┐
│ Claude #1   │ ───HTTP───────> │                  │              │              │
├─────────────┤                 │ MCP Server :56688│ <──SignalR──>│ Unity Plugin │
│ Claude #2   │ ───HTTP───────> │                  │              │              │
└─────────────┘                 └──────────────────┘              └──────────────┘
```

## Configuration Files

| File                                             | Purpose                       |
| ------------------------------------------------ | ----------------------------- |
| `.mcp.json`                                      | Claude Code MCP configuration |
| `start-mcp-server.bat`                           | Server startup script         |
| `Assets/Resources/AI-Game-Developer-Config.json` | Unity plugin settings         |

## Notes

- Keep the terminal window open - closing it stops the server
- Server runs on port 56688 (HTTP mode)
- Multiple Claude Code sessions can connect simultaneously
- If Unity is already open, it should auto-reconnect

## Troubleshooting

- If connection fails, ensure port 56688 is not in use
- Check Windows Firewall settings
- Verify the server executable exists in `Library/mcp-server/`
