# OpenAI-compatible shim for opencode

Stdlib-only facade over `opencode serve`: lets any OpenAI client drive opencode-only models (e.g. Luna subscription models; opencode free tier rejects third-party clients).

- One session per (chat, provider, model) — no collisions on fan-out compares.
- Replay conversation into a fresh session on missing/evicted/rejected sessions, retry once.
- Empty toolset sent — chat UI can't trigger file read/write.
- Images pass through as data-URL parts, fetched once, size-capped.