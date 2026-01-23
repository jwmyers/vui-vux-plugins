---
name: start-unity-mcp
description: Start the Unity MCP server before opening Unity
allowed-tools: "*"
---

# Start Unity MCP Server

Start the Unity MCP server using the project's startup script. The server must be running before Unity can connect.

## Process

1. Check if server is already running (port 56688)

2. Start the MCP server inside the zero-day-attack root folder:

   ```bash
   run start-mcp-server.bat
   ```

3. Check to see if the server is running

4. If confirmed, notify user. If not, enter troubleshooting with the `mcp-advisor` agent

## Architecture

```text
┌─────────────┐                 ┌──────────────────┐              ┌──────────────┐
│ Claude #1   │ ───HTTP───────> │                  │              │              │
├─────────────┤                 │ MCP Server :56688│ <──SignalR──>│ Unity Plugin │
│ Claude #2   │ ───HTTP───────> │                  │              │              │
└─────────────┘                 └──────────────────┘              └──────────────┘
```

## Configuration Files

| File                                                                                           | Purpose                       |
| ---------------------------------------------------------------------------------------------- | ----------------------------- |
| `C:/Users/jon/.claude/plugins/marketplaces/vui-vux/plugins/zero-day-dev/mcp.json`              | Claude Code MCP configuration |
| `C:/Users/jon/Documents/GitHub/zero-day-attack/start-mcp-server.bat`                           | Server startup script         |
| `C:/Users/jon/Documents/GitHub/zero-day-attack/Assets/Resources/AI-Game-Developer-Config.json` | Unity plugin settings         |

## Notes

- Keep the terminal window open - closing it stops the server
- Server runs on port 56688 (HTTP mode)
- Multiple Claude Code sessions can connect simultaneously
- If Unity is already open, it should auto-reconnect

## Troubleshooting

- If connection fails, ensure port 56688 is not in use
- Check Windows Firewall settings
- Verify the server executable exists in `C:/Users/jon/Documents/GitHub/zero-day-attack/Library/mcp-server/win-x64`
