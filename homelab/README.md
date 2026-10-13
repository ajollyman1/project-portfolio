# Self-hosted homelab

A Linux box I keep at home that's replaced about a dozen subscriptions. It serves my own AI models, runs my phone and calendar as agent tools, and does the usual media-server job. The honest reason I built it out this far is that I wanted the privacy *and* I wanted the excuse to learn how all these pieces actually fit together.

## What's running on it

- **Local AI** — text models served on the GPU with **llama.cpp**, speech-to-text with **whisper.cpp**, and a **Kokoro** TTS voice, all fronted by a self-hosted **OpenWebUI**.
- - A self-hosted **odysseus** AI-workspace I installed and have been extending with local patches.
  - - **Agent tooling** — an opencode headless server behind an OpenAI-compatible shim, so ordinary chat clients can reach models that are otherwise locked to it.
    - - **Phone + calendar** exposed as MCP tools the AI can call (see the folders below).
      - - **Media + infra** — a Caddy reverse proxy, a Tailscale/netbird mesh for remote access, a few KVM/libvirt VMs, and the usual `*arr` stack (Radarr/Sonarr/Jellyfin) routed through a VPN gateway.
       
        - Everything is held together with **Docker Compose** stacks and **systemd** user services, so a reboot brings it all back without me babysitting it.
       
        - ## The parts I'm proud of
       
        - The whole thing is deliberately boring on the outside and only interesting where it had to be. The interesting parts are the little bridges — the shims and MCP servers that let a language model act on real things (my phone, my calendar) instead of just talking about them. Those live in the sibling folders:
       
        - - [`phone-mcp`](../phone-mcp/README.md) — let an LLM agent drive my Android phone
          - - [`voiceapi`](../voiceapi/README.md) — an OpenAI-compatible voice API, fully local
            - - [`calendar-mcp`](../calendar-mcp/README.md) — my calendar, exposed as an MCP tool
              - - [`opencode-oai-shim`](../opencode-oai-shim/README.md) — OpenAI client support for models that only opencode can reach
