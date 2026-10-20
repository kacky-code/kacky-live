# Kacky Live

Read-only streamer overlays and a Twitch surface for Kacky events.

Kacky Live is an open source project. It reads public `GET /v1/...` endpoints from the
[KackyGG API](https://api.kacky.gg/v1) and renders them for streamers. It never writes to the API,
the game servers or the kontrol stream contract.

## Status

Planning. Phase 0 is a one-page spec and a mockup. There is no application code yet.

See the [open issues](https://github.com/kacky-code/kacky-live/issues) for the current work.

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

Widgets:

- Event name and day N of M.
- Current map, author time and world record.
- Top 5 records on the current map.
- The next maps in the server queue.
- Top donors over the last 90 days.

The overlay keeps the last good state when the API fails. It never shows an error or a stack trace
on stream.

### Phase 2: Twitch panel extension

Optional, and only after phase 1 is used by a real streamer. It reuses the same data layer and adds
a Twitch configuration page.

## Non-goals

- No new backend endpoints.
- No admin panel, auth or user accounts.
- No live donation stream in phase 1. The public top-donors endpoint is polled.
- No scraping and no undocumented endpoints.
- No changes to `kacky-ds` or the main website.
- No production database, SSH, vault or deploy access.

## Documentation

- [`CONTRIBUTING.md`](CONTRIBUTING.md): the workflow and the review rules.
- [`docs/SPEC-TEMPLATE.md`](docs/SPEC-TEMPLATE.md): the phase 0 deliverable.
- [`docs/API-NOTES.md`](docs/API-NOTES.md): the public endpoints and their shapes.

## Contributing

Contributions are welcome. Open an issue before a large change, work on a branch and open a pull
request against `main`. See [`CONTRIBUTING.md`](CONTRIBUTING.md) for the details.

## Maintainers

- [@Thorbenl](https://github.com/Thorbenl)
- [@bompi-me](https://github.com/bompi-me)

Only the maintainers merge to `main`. Everyone else can contribute through forks and pull requests.

## Security

Do not open a public issue for a security problem. See [`SECURITY.md`](SECURITY.md).

## Licence

[GNU General Public License v3.0](LICENSE).
