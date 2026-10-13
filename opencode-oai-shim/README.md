# OpenAI-compatible shim for opencode

I wanted to point a normal chat client — one that speaks the OpenAI API — at models that are only reachable through **opencode**. Some subscription models (the "Luna" ones) are only served on an API that generic clients don't understand, and opencode's free tier rejects third-party clients outright. This is a small **OpenAI-compatible facade** that sits in front of a local `opencode serve` and translates, so any OpenAI client can drive models it otherwise couldn't.

Written with the **standard library only** — no dependencies.

## The fiddly bits

- **Session isolation.** opencode won't accept two messages to the same session at once, so the shim keeps one session per (chat, provider, model). A client that fans one message out to several models for a side-by-side compare gets a separate session each, and nothing collides.
- **Recovery.** Sessions go missing — first turn, eviction, an upstream rejection. When that happens the shim replays the whole conversation into a fresh session and retries the send once, instead of failing the request.
- **Safety.** It deliberately sends an empty toolset, so a chat UI can never get the agent to read or write my files just by asking nicely.
- **Images** pass through as data-URL file parts, fetched once and capped in size so a malicious or enormous URL can't blow up the request.
