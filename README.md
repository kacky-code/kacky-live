# Kacky Live

[![License: GPL-3.0](https://img.shields.io/badge/license-GPL--3.0-FF7800)](LICENSE)

Read-only broadcast overlays for Kacky events. Kacky Live gives streamers a clean, always-current board for the current map, the top records, the queue and the top donors, without another tab on stream.

Kacky Live is for the streamers who cover Kacky, the viewers who follow every map, and the developers who want to help. It reads public `GET` endpoints from the KackyGG API and never writes to the API, the game servers or the kontrol stream contract. The endpoints and their shapes live in [`docs/API-NOTES.md`](docs/API-NOTES.md), and the event itself lives at [kacky.gg](https://kacky.gg).

**Status:** planning. Phase 0 is a one-page spec and a mockup. There is no application code yet. See the [roadmap](#roadmap) or the [open issues](https://github.com/kacky-code/kacky-live/issues).

## Roadmap

| Phase | Goal | Status |
|---|---|---|
| [Phase 0: spec and mockup](https://github.com/kacky-code/kacky-live/milestone/1) | Agree on the layout, data and failure states before code | In progress |
| [Phase 1: overlay MVP](https://github.com/kacky-code/kacky-live/milestone/2) | OBS browser source with the widgets below | Planned |
| [Phase 2: Twitch panel extension](https://github.com/kacky-code/kacky-live/milestone/3) | The same data layer on a Twitch panel, only after the overlay is proven | Optional |

## Why a separate app

- Zero blast radius. No writes, no database, no secrets and no deploy rights on the core stack.
- The data already exists on the public API.
- The overlay can be tested on live KR7 streams without touching the event.

## What we are building

### Phase 1: OBS overlay

A 1920x1080 transparent browser source for OBS. The streamer configures it with a URL:

```
https://<host>/overlay?server=<server-login>&player=<player-login>
```

`server` is required. `player` is optional: when it is set, the streamer's own record is highlighted in the top 5. Leave it out to show the full board.

Widgets:

- Event name and day N of M.
- Current map, author time and world record.
- Top 5 records on the current map.
- The next maps in the server queue.
- Top donors over the last 90 days.

The overlay keeps the last good state when the API fails. It never shows an error or a stack trace on stream.

### Phase 2: Twitch panel extension

Optional, and only after phase 1 is used by a real streamer. It reuses the same data layer and adds a Twitch configuration page.

## Non-goals

- No new backend endpoints.
- No admin panel, auth or user accounts.
- No live donation stream in phase 1. The public top-donors endpoint is polled.
- No scraping and no undocumented endpoints.
- No changes to `kacky-ds` or the main website.
- No production database, SSH, vault or deploy access.

## Documentation

- [`CONTRIBUTING.md`](CONTRIBUTING.md): the workflow and the review rules.
- [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md): the community standard.
- [`docs/SPEC-TEMPLATE.md`](docs/SPEC-TEMPLATE.md): the phase 0 deliverable.
- [`docs/API-NOTES.md`](docs/API-NOTES.md): the public endpoints and their shapes.

## Contributing

Contributions are welcome. The best first step is issue [#10, OBS setup docs and URL config page](https://github.com/kacky-code/kacky-live/issues/10): the OBS setup section can land before the overlay scaffold, so it is a good place to start.

- Browse the [`good first issue`](https://github.com/kacky-code/kacky-live/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22) and [`help wanted`](https://github.com/kacky-code/kacky-live/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22) labels.
- Read [`CONTRIBUTING.md`](CONTRIBUTING.md) for the branch, review and writing rules.
- Open an issue before a large change so we can agree on the scope.

## Maintainers

- [@Thorbenl](https://github.com/Thorbenl)
- [@bompi-me](https://github.com/bompi-me)

Only the maintainers merge to `main`. Everyone else can contribute through forks and pull requests.

## Security

Do not open a public issue for a security problem. See [`SECURITY.md`](SECURITY.md).

## Licence

[GNU General Public License v3.0](LICENSE).
