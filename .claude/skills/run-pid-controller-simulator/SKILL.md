---
name: run-pid-controller-simulator
description: Run, launch, start, screenshot, or verify the PID Controller Simulator web app. Use when asked to run the app, take a screenshot, or confirm a change works.
---

# Run: PID Controller Simulator

Single-file web app (`index.html`) — pure HTML/CSS/JS with Canvas charts, zero npm dependencies. Serve the project root over HTTP and drive with preview tools.

All paths below are relative to the project root (`pid-controller-sim/`).

## Prerequisites

Node.js (for `npx serve`). No `npm install` needed — there are no dependencies.

## Build

None. Single HTML file, no build step.

## Run (agent path) — preview tools

1. Ensure `.claude/launch.json` exists at the **user home directory** (not project root) with:

```json
{
  "version": "0.0.1",
  "configurations": [
    {
      "name": "pid-sim",
      "runtimeExecutable": "npx",
      "runtimeArgs": ["serve", "-l", "3456", "-s", "Downloads/pid-controller-sim"],
      "port": 3456
    }
  ]
}
```

2. Start the server and resize viewport:

```
preview_start  name="pid-sim"
preview_resize serverId=<id> width=1400 height=900
```

3. Interact and screenshot:

```
preview_click      serverId=<id> selector=".auto-tune-btn"
preview_click      serverId=<id> selector="#btn-second"
preview_screenshot serverId=<id>
```

Key selectors:
- `#btn-first` / `#btn-second` — plant type toggle
- `#sl-K`, `#sl-tau`, `#sl-wn`, `#sl-zeta` — plant parameter sliders
- `#sl-kp`, `#sl-ki`, `#sl-kd` — PID gain sliders
- `.auto-tune-btn` — Ziegler-Nichols auto-tune
- `#chart-step`, `#chart-error` — Canvas chart elements

## Run (human path)

Open `index.html` directly in a browser — no server needed for local use:

```
start index.html
```

Or serve it:

```
npx serve -l 3456 -s .
```

Then open http://localhost:3456

## Gotchas

- **Viewport must be wide enough.** At narrow widths the grid collapses to single-column and charts shrink. Use `preview_resize` with width >= 1200 before screenshotting.
- **Canvas charts don't show in `preview_snapshot`.** The accessibility tree shows `Canvas` nodes but no drawn content. Use `preview_screenshot` to verify chart rendering.
- **Slider float precision.** HTML range inputs can produce values like `2.0999999` instead of `2.1`. The display rounds correctly but the raw slider value may look odd in snapshots.
- **Dark background.** The app uses `#0f172a` background. A default-size preview screenshot may appear all-black — resize the viewport first.

## Troubleshooting

| Symptom | Fix |
|---------|-----|
| Blank/black page in preview | Resize viewport to 1400x900 before screenshotting |
| `npx serve` not found | Install Node.js — `npx` ships with it |
| Charts not rendering | Check console for JS errors. Canvas needs nonzero width — ensure the container is visible |
