# Project Portfolio

A grab-bag of things I've built — some software, some hardware. The software half is mostly a self-hosted homelab and the agent tooling I run on it; the hardware half is electric go-kart / e-bike / battery builds.

## Software, AI & self-hosting

- **[`homelab`](homelab/README.md)** — the Linux server everything below runs on: local LLM/speech models, Docker Compose, Caddy, Tailscale, KVM. Best starting point.
- - **[`phone-mcp`](phone-mcp/README.md)** — let an AI agent drive my Android phone (tap, swipe, type, read the screen) over ADB, exposed as an MCP tool. Safety-first: no shell, a kill switch, loopback only.
  - - **[`voiceapi`](voiceapi/README.md)** — an OpenAI-compatible speech API (STT + TTS) backed entirely by local models.
    - - **[`calendar-mcp`](calendar-mcp/README.md)** — my CalDAV calendar exposed to agents as an MCP tool, with write-verification so "it's booked" is actually true.
      - - **[`opencode-oai-shim`](opencode-oai-shim/README.md)** — a dependency-free OpenAI-compatible facade that lets any chat client reach models only `opencode` can.
        - - **[`phone-ui`](phone-ui/README.md)** — an installable PWA front-end for phone-mcp, with the kill switch one tap away.
         
          - ## Hardware
         
          - - **[`homemade-spot-welder`](homemade-spot-welder/README.md)** — a spot welder built from a car battery and MOSFETs from a dead e-bike controller. Unreliable, but it welded.
            - - **[`gokart-battery-pack`](gokart-battery-pack/README.md)** — a 72V, 20S10P pack built from recycled 18650 cells for a 3kW go-kart, with 3D-printed holders for cooling and isolation.
              - - **[`go-kart`](go-kart/README.md)** — a converted 3kW electric go-kart: the controller saga, a wooden battery box, and a lot of frame repair.
                - - **[`first-ebike`](first-ebike/README.md)** — my first electrical/mechanical build: a 36V/500W mid-drive e-bike conversion.
