<div align="center">
  <img src="assets/banner.svg" width="100%" alt="AirSec Preview — follow every path and pivot at every interaction">

  [![Live preview](https://img.shields.io/badge/live-airsec.akeyo.io-15b8cb)](https://airsec.akeyo.io)
  [![GitHub Pages](https://img.shields.io/badge/host-GitHub%20Pages-222)](https://airsec.akeyo.io)
  [![Self-contained](https://img.shields.io/badge/runtime-self--contained-63d796)](#the-part-that-should-stop-you)
  [![Focused tests](https://img.shields.io/badge/focused%20regressions-88%20passing-e9b84f)](#trust-is-observed)
  [![License: MIT](https://img.shields.io/badge/license-MIT-4d8fd8)](LICENSE)
  [![GitHub stars](https://img.shields.io/github/stars/fire17/AirSecPreview?style=social)](https://github.com/fire17/AirSecPreview/stargazers)
</div>

## For agents

Open the public artifact directly:

```bash
open https://airsec.akeyo.io
```

| When you are told… | Do this |
|---|---|
| “Show the AirSec preview” | Open `https://airsec.akeyo.io` |
| “Inspect the published artifact” | Read [`index.html`](index.html) and [`terminal.json`](data/facility/terminal.json) |
| “Change the production system” | Stop: this repo is the showcase export, not the private production source |

The authority for public behavior is the checked-in `index.html`. Re-read it from disk; do
not infer production architecture from this static replay, and never publish private AirSec
source files into this repository.

<div align="center">
  <i>A security trail should explain the whole story, not merely point at the last frame.</i>

  **[Open the demo](https://airsec.akeyo.io)** · **[Why it is self-contained](#the-part-that-should-stop-you)** · **[Interaction model](#interaction-model)** · **[Trust](#trust-is-observed)**
</div>

## The part that should stop you

This is a fully interactive terminal replay in one public artifact—no cross-origin tunnel,
no local AirSec server, and no laptop that must remain online.

- Person A, person B, BAG-1, and authorised security staff retain distinct visual identities from the first replay frame.
- Orange and red heartbeat rings are driven by scenario events, including the P2 pickup.
- A selected entity exposes its whole path; an interaction dot reveals and opens related paths.
- Any selected entity can be pinned into a durable watched list and reopened at its live or last-known position.
- Terminal 1 Wing A is one small live zone inside a 400×230 m airport campus, with current/nearby/all event scopes.
- The campus includes distinct terminals, concourses, aprons, stands, taxiways, runways, service roads, and moving aircraft.
- Desktop operators can collapse or resize the operations rail; phones get a dedicated full-screen field layout.
- The map automatically pulls back to the full airport 30 seconds after the 95-second scenario ends.

> [!IMPORTANT]
> The public artifact is an honest deterministic showcase. It does not claim to be a live airport feed or the private production backend.

```mermaid
flowchart LR
  S["Verified scenario clock"] --> W["Terminal world"]
  W --> T["Full historical trails"]
  W --> A["Severity-aware alerts"]
  T --> H["Hover interaction"]
  H --> B["Related path branches"]
  A --> F["Wing-scoped event rail"]
  style S fill:#102a35,stroke:#22c7dc,color:#eefcff
  style T fill:#2a2110,stroke:#e9b84f,color:#fff7dc
  style B fill:#2c1320,stroke:#ed4055,color:#ffe8ec
```

## Quickstart

Open [airsec.akeyo.io](https://airsec.akeyo.io), click a person or item, then hover over its
trail and interaction dots. Use the mouse wheel to zoom, drag anywhere to pan, change replay
speed from 0.25× to 4×, and use the traffic slider to tune terminal density.

![AirSec red-alert tracking state](assets/preview.png)

## Interaction model

| Capability | What it does |
|---|---|
| Full-path selection | Keeps the complete route visible from entry through exit |
| Trail hover | Reveals scenario time, observed segment, and world position |
| Interaction junctions | Uses smaller type-colored dots for drops, touches, pickups, transfers, and groups |
| Branch pivot | Reveals related paths in distinct colors and lets the operator hop to them |
| Severity tracking | Starts orange at drop/abandonment and red after the non-owner pickup |
| Security semantics | Records authorised staff contact without generating the illicit-contact alert |
| Airport navigation | Fits Terminal 1 Wing A, Terminal 2, Terminal 3, the north satellite, international terminal, airside, or the full airport; free zoom/pan remains available |
| Airport operations | Animates top-down aircraft on the airfield and identifies parked/taxiing state on hover |
| Traffic density | Adds a deterministic high-density terminal population controlled as people per 1,000 m², so larger public areas naturally carry more traffic |
| Watched entities | Persists operator pins on-device, marks them on-map, and jumps to live or last-known position |
| Adaptive operations rail | Collapses, pointer-resizes, keyboard-resizes, persists its state, and refits the map continuously |
| Mobile field mode | Uses a full-screen map, one-finger pan, two-finger pinch, contained sheets, and a five-action safe-area dock |
| Event scope | Filters the right rail to current wing by default, nearby wings, or all wings |

<details>
<summary><b>What the static export includes</b></summary>

- The full airport campus plus Terminal 1's detailed floorplan, zones, walls, and camera coverage geometry.
- The 95-second A/B/BAG-1 scenario plus the 30-second post-scenario observation window.
- Additional Terminal 2, Terminal 3, north satellite, and international-terminal movements and interactions.
- Client-side timeline and custody evidence used by the dossier and interaction branches.
- A deterministic loop so the public demo remains usable without a backend.

</details>

## How this release was made

```mermaid
flowchart TD
  P["Private AirSec preview"] --> E["Selective static export"]
  E --> V["Syntax + regression checks"]
  V --> B["Headless browser interaction probe"]
  B --> G["GitHub Pages + custom domain"]
  style P fill:#102a35,stroke:#22c7dc,color:#eefcff
  style V fill:#2a2110,stroke:#e9b84f,color:#fff7dc
  style G fill:#182c20,stroke:#63d796,color:#e9fff1
```

The release was deliberately staged outside the production repository. The browser probe
selected A, clipped its trail to the current replay instant with three visible interactions,
revealed BAG-1 as a related branch, proved current-wing filtering hid off-wing alerts,
verified traffic-density changes and plain-drag panning, and measured accelerated scenario
advance at 4×. A separate 390×844 field-operator pass verified five touch targets, watched
state across reload, one-finger map navigation, bounded sheets, and a dossier that stays in-view.

Defects caught before publication included the need for a static backend seam, carried-item
marker overlap, sandbox-only test database failures, and a canvas/page coordinate mismatch
in the first interaction probe.

## Safety and undo

| Concern | Release behavior |
|---|---|
| Production source | Never copied into this public repository |
| Secrets and credentials | None included in the artifact |
| Backend dependency | None; the public replay runs in the browser |
| Rollback | Revert the Pages repository commit or remove its custom-domain binding |
| Local AirSec project | Left in place and untouched by the deployment staging step |

## Trust is observed

- JavaScript syntax validation passed.
- The focused AirSec pattern/demo-server regression suite passed: 88 tests.
- A real headless Chrome run passed selection, full-trail loading, interaction branching,
  watch persistence, rail collapse/resize, wing filtering, speed/traffic control, desktop and
  touch panning, mobile sheets, and the timed full-airport overview with zero page errors.
- The public URL, TLS certificate, redirects, and served content are rechecked after each publish.

> [!NOTE]
> These receipts validate this showcase path. They are not detector, ReID, or production-airport performance claims.

<div align="center">

## Follow the whole story

If a system should preserve context instead of collapsing reality to the latest alert, this
preview is the argument you can click.

[![Star History Chart](https://api.star-history.com/svg?repos=fire17/AirSecPreview&amp;type=Date)](https://star-history.com/#fire17/AirSecPreview&Date)

Released under the [MIT License](LICENSE). · [Launch AirSec Preview](https://airsec.akeyo.io)

<sub><i>Every path stays visible. Every pivot keeps its evidence.</i></sub>
</div>
