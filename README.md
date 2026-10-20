# Kacky Live

[![License: GPL-3.0](https://img.shields.io/badge/license-GPL--3.0-FF7800)](LICENSE)

Clean, read-only broadcast overlays for [Kacky](https://kacky.gg) events. Kacky Live gives streamers an always-current board for the active map, top records, server queue, and top donors—right inside OBS without needing another browser tab on screen.

Built for Kacky streamers and viewers, Kacky Live runs entirely in the browser on top of the public KackyGG API ([`docs/API-NOTES.md`](docs/API-NOTES.md)). Because it is lightweight and strictly read-only, anyone can run it locally, test against live data, and contribute widgets without needing backend credentials or server access.

**Current Status:** Planning ([Phase 0](https://github.com/kacky-code/kacky-live/milestone/1)). We are locking in the layout spec and mockup before scaffolding the app. Check the [open issues](https://github.com/kacky-code/kacky-live/issues) to jump in.

## Roadmap

| Phase | Goal | Status |
|---|---|---|
| [Phase 0: spec and mockup](https://github.com/kacky-code/kacky-live/milestone/1) | Finalize layout, data polling, and fallback states before writing code | In progress |
| [Phase 1: overlay MVP](https://github.com/kacky-code/kacky-live/milestone/2) | Ship the 1920x1080 OBS browser source with core widgets | Planned |
| [Phase 2: Twitch panel extension](https://github.com/kacky-code/kacky-live/milestone/3) | Bring the same data layer to a Twitch panel once the OBS overlay is proven | Optional |

## What We're Building

### Phase 1: OBS Overlay

A `1920x1080` transparent browser source for OBS, configured entirely via URL parameters:

```text
https://<host>/overlay?server=<server-login>&player=<player-login>
```

- `server` (required): The Kacky server login to track.
- `player` (optional): Highlights the streamer's own record in the top 5 board when set.

#### Core Widgets

- **Event Header:** Active event title and current day (Day N of M).
- **Map Card:** Current map number/name, author time, and world record.
- **Top 5 Records:** Live top 5 leaderboard for the active map.
- **Server Queue:** Next maps coming up on the server.
- **Top Donors:** Top supporters over the last 90 days.

#### Stream-Safe by Design

- **Quiet visuals:** High contrast for readability over Trackmania stadium surfaces, with zero distracting animations during runs.
- **Graceful fallbacks:** If an API request fails or times out, the overlay holds the last known good state and never flashes error popups or stack traces on stream.

### Phase 2: Twitch Panel Extension

Once the OBS overlay is battle-tested on live streams, Phase 2 reuses the same API client to power a viewer-facing Twitch panel extension.

## Documentation

- [`CONTRIBUTING.md`](CONTRIBUTING.md) – Workflow, design rules, and PR guidelines.
- [`docs/API-NOTES.md`](docs/API-NOTES.md) – Public KackyGG `/v1` endpoints, payload fields, and polling intervals.
- [`docs/SPEC-TEMPLATE.md`](docs/SPEC-TEMPLATE.md) – Structure for the Phase 0 layout and state spec.
- [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md) – Community guidelines.

## Contributing

We want Kacky Live to be easy and fun to contribute to. A great place to start right now is Issue [#10: OBS setup docs and URL config page](https://github.com/kacky-code/kacky-live/issues/10), or weighing in on the layout spec in Issue [#1](https://github.com/kacky-code/kacky-live/issues/1).

- Browse [`good first issue`](https://github.com/kacky-code/kacky-live/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22) and [`help wanted`](https://github.com/kacky-code/kacky-live/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22).
- Check [`CONTRIBUTING.md`](CONTRIBUTING.md) before opening a pull request.

## Maintainers

Maintained by [@Thorbenl](https://github.com/Thorbenl) and [@bompi-me](https://github.com/bompi-me).

## Security & Licence

Please report security issues privately via [SECURITY.md](SECURITY.md). Licensed under the [GNU General Public License v3.0](LICENSE).
