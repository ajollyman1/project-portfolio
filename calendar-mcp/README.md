# Calendar over MCP

Once I had an AI agent, the obvious next question was whether it could actually manage my life instead of just advising me on it. The first thing I handed it was my calendar.

  My calendar lives on a self-hosted **Radicale** server (CalDAV). This turns it into an **MCP** tool by wrapping the CalDAV backend and exposing it as a Streamable-HTTP MCP server, so the agent can list, create, move, and delete events conversationally.

  ## The part I'd do again

  The bit I'm glad I thought about is **write-verification**. LLMs are confident even when they're wrong, and "I've added that to your calendar" is a nasty thing to get wrong — you just don't show up. So after any write the server reads the event back from CalDAV and only reports success once the change is actually there. If the backend silently dropped or mangled it, the agent finds out *now* instead of me finding out a week later.

  It's bearer-token authenticated and bound to loopback like the others, and I added a synthetic `get_current_time` tool because the model kept reasoning about dates without ever being told what "now" is.
