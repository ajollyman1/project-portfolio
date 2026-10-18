# Phone control over MCP

Android phone exposed as MCP tools (tap, swipe, type, keys, launch, view intents, read screen, screenshot) over wireless ADB.

## Key idea

LLMs are text. Screen is translated to a compact text view tree (uiautomator dump) so the model picks real controls instead of guessing pixel coords.

## Safety

- No shell tool — input + read only.
- Kill switch (pause file) checked by every mutating tool.
- Bearer auth, loopback only. Off-network deep-links fall back to ntfy notification.

## phone-ui

Installable PWA front-end: screenshots, quick actions, one-tap kill switch. Runs as systemd user services; separate service keeps wireless ADB alive.