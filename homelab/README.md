# Self-hosted homelab

A Linux box I keep at home that's replaced about a dozen subscriptions. It serves my own AI models, runs my phone and calendar as agent tools, and does the usual media-server job. The honest reason I built it out this far is that I wanted the privacy *and* I wanted the excuse to learn how all these pieces actually fit together.

## What's running on it

- **Local AI** — text models served on the GPU with **llama.cpp**, speech-to-text with **whisper.cpp**, and a **Kokoro** TTS voice, all fronted by a self-hosted **OpenWebUI** (also running Chatterbox TTS).
- A self-hosted **odysseus** AI-workspace I installed and have been extending with local patches (with its own SearXNG, ChromaDB, and ntfy).
- **Agent tooling** — an opencode headless server behind an OpenAI-compatible shim, so ordinary chat clients can reach models that are otherwise locked to it.
- **Phone + calendar exposed as MCP tools** the AI can call — [`phone-mcp`](../phone-mcp/README.md) / [`phone-ui`](../phone-ui/README.md) are **ongoing** and in daily use; [`calendar-mcp`](../calendar-mcp/README.md) too.
- **The media server** — see below.

## Media server

The biggest continuous project. It's a single Docker Compose stack (`/opt/mediaserver`) running the full automate-then-serve pipeline on a 1.8 TB drive:

- **Jellyfin** — the server itself. Movies, TV, music, and downloaded videos live on `/mnt/bigstorage/data/media` (~450 GB) and get served to every device in the house; Jellyfin runs with FFmpeg for transcoding and hardware video support.
- **Sonarr · Radarr · Lidarr** — the `*arr` automation: TV, movies, and music respectively. They watch for releases, hand them to the downloader, then import and rename into the library.
- **Prowlarr** — one place to manage all the indexers, syncs them into each `*arr`.
- **Bazarr** — automatic subtitles for everything.
- **qBittorrent behind a Mullvad (WireGuard) gateway** — the interesting bit of the whole stack. Downloads don't run in the container's own network; **gluetun** holds the WireGuard tunnel (Mullvad, Auckland) and qBittorrent shares its network namespace, so *all* torrent traffic is forced through the VPN and a dead tunnel means no leaks. FlareSolverr sits beside it to get past Cloudflare-protected indexers, and the `*arr`s + Bazarr reach qBittorrent's API through the gateway with `extra_hosts` routing.
- **metube** — self-hosted YouTube/audio downloader, pointed at the same VPN HTTP proxy (its downloads land in the library for Jellyfin to pick up).
- **Samba** — shares the library out to the LAN.

Downloads land in `/mnt/bigstorage/data/torrents` (~84 GB live) before they're imported. The rest of the box: a few **KVM/libvirt** VMs (~290 GB of virtual disks on the same drive), and everything above is held together with Docker Compose stacks and **systemd** user services so a reboot brings it all back without me babysitting it.

## Ops & remote access

- **Caddy** reverse proxy fronts the services, with **netbird** (a WireGuard mesh VPN) for remote access — no Tailscale, and nothing but the proxy exposed to the internet.
- Both run `restart: unless-stopped` / as services, so this thing has been up for weeks at a time.

## The parts I'm proud of

The whole thing is deliberately boring on the outside and only interesting where it had to be. The interesting parts are the little bridges — the shims and MCP servers that let a language model act on real things (my phone, my calendar) instead of just talking about them, and the VPN-gated download pipeline, where the design constraint was "this can never leak a plaintext connection" rather than "make it fast". Those live in the sibling folders:

- [`phone-mcp`](../phone-mcp/README.md) — let an LLM agent drive my Android phone (**ongoing**)
- [`phone-ui`](../phone-ui/README.md) — the PWA front-end for the above (**ongoing**)
- [`voiceapi`](../voiceapi/README.md) — an OpenAI-compatible voice API, fully local
- [`calendar-mcp`](../calendar-mcp/README.md) — my calendar, exposed as an MCP tool
- [`opencode-oai-shim`](../opencode-oai-shim/README.md) — OpenAI client support for models that only opencode can reach
