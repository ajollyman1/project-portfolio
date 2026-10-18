# Calendar over MCP

Radicale (CalDAV) wrapped as a Streamable-HTTP MCP server: list/create/move/delete events. Write-verification reads back after every write and only reports success if it landed. Bearer auth, loopback only. Includes `get_current_time` tool (model kept reasoning about dates without "now").