# Phone control over MCP

I wanted to see whether an AI agent could actually *use* my phone the way I do — open an app, read what's on screen, tap the right thing — instead of just telling me which button to press. So I turned my Android phone into a tool the agent can call.

The phone talks to the server over ADB wireless debugging and is exposed as an **MCP server**. The agent gets tools for tapping, swiping, typing, pressing keys, launching apps, firing VIEW intents, reading the screen, and taking screenshots.

## The interesting problem

A language model is *text*. It can't look at a screenshot and go "tap the red button", and it definitely can't guess pixel coordinates reliably. The trick was to translate the screen into something a text-only model can reason about: after every action the tool runs `uiautomator` to dump the view tree and hands the model a **compact text description of what's on screen** — the buttons that exist, the text they contain, the things that are actually clickable. That one idea is what makes the whole thing work, because now the model is picking from a list of real controls instead of hallucinating coordinates.

## Safety

Giving a model my phone is a bit scary, so it's locked down on purpose:

- **No shell tool.** The agent can send *input* (tap/swipe/text/keys) and read the screen. It cannot run arbitrary commands on the phone.
- **A kill switch** — a pause file that every mutating tool checks first, so saying "stop" (by voice, from Tasker, or from the model itself) takes effect immediately, even mid-way through a multi-step run.
- Bearer-token auth, bound to loopback only. Nothing about the phone is exposed publicly.

When the phone is off the network, deep-link actions fall back to pushing an **ntfy notification** with a tappable link, so "open this in the app" still works — I just finish the tap.

## phone-ui

Because firing tools at a shell is miserable, I also built a little installable **PWA** ([`phone-ui`](../phone-ui/README.md)) as a front-end over it — a dashboard with screenshots, a kill-switch button, and quick actions that I can add to my phone's home screen.

Both pieces run as plain `systemd` user services, with a second service whose only job is keeping the wireless ADB connection alive.
