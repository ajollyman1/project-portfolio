# Self-hosted homelab

Linux box at home replacing ~a dozen subscriptions: local AI models, phone/calendar agent tools, media server. Jarvis-style personal assistant running entirely on my own hardware.

## Local AI

- **OpenWebUI** — chat UI over local backends: llama.cpp (Qwen 9B/27B, one at a time), whisper.cpp STT, Kokoro/Chatterbox TTS, Ollama.
- **pi** — coding-agent CLI over the same models with read/bash/edit/write + MCP tools; replacing the odysseus AI workspace.

## Media server

Docker Compose stack (`/opt/mediaserver`) on a 1.8 TB drive:
- Jellyfin (serve), Sonarr/Radarr/Lidarr (automate), Prowlarr (indexers), Bazarr (subs).
- qBittorrent behind gluetun (Mullvad WireGuard) — all torrent traffic forced through VPN; FlareSolverr for Cloudflare indexers.
- metube (YouTube downloader), Samba (LAN share).
- ~450 GB media, ~84 GB torrents. Windows VM (KVM, ~290 GB) gets first claim on GPU; streamed to laptop via Sunshine/Moonlight.

## Ops & remote access

- Caddy reverse proxy; netbird (WireGuard mesh) for remote access; nothing else exposed.
- Services run `restart: unless-stopped` or as systemd user services.

## Related

- [phone-mcp](../phone-mcp/README.md), [phone-ui](../phone-ui/README.md), [voiceapi](../voiceapi/README.md), [calendar-mcp](../calendar-mcp/README.md), [opencode-oai-shim](../opencode-oai-shim/README.md)