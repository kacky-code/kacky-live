# API Notes

The overlay reads the public KackyGG API. All paths below are under `/v1`.

| Environment | Base URL |
|---|---|
| Production | `https://api.kacky.gg/v1` |
| Development | `https://api-dev.kacky.gg/v1` |

## Conventions

- **Authentication:** None required. All endpoints are unauthenticated public `GET` requests.
- **Payload Shape:** Paginated endpoints return `{ data, meta }`.
- **Polling Intervals:** We suggest 20s for active game state (current map, records, queue) and 60s for event metadata or donor standings.
- **Inactive / Fallback States:** Inactive events or private servers return `404`. Hold the last known good state or hide the affected widget cleanly rather than displaying errors on stream.
- **OpenAPI:** OpenAPI docs are internal and not served in production.

## Endpoints

### `GET /events/active`

Returns the active event or `404`.

Fields: `id`, `edition`, `name`, `eventType`, `startTime`, `endTime`, `isActive`.

### `GET /servers/live`

Returns the public live server list. Private servers are hidden.

Fields: `login`, `name`, `status`, `playerCount`, `gameType`, `eventId`, `eventType`,
`eventFamily`, `currentMap` (`mapUid`, `name`, `mapNumber`) or `null`.

### `GET /servers/{login}/maps`

Returns the current map and the queue.

Fields: `currentMap` (`MapDto` or `null`), `nextMaps` (`MapDto[]`).

### `GET /maps/{mapNumber}`

Returns one map. Fields used by the overlay: `name`, `author`, `authorTime` (milliseconds),
`mapNumber`, `gameType`, `imageUrl`, `totalFinishers`.

### `GET /maps/{mapNumber}/records`

Paged records for one map.

Query: `limit`, `offset`, `sortBy` (`rank`, `score`, `nickname`, `finishCounter`,
`lastImprovedAt`), `sortDirection`.

Fields per row: `rank`, `playerId`, `nickname`, `customNickname`, `score` (milliseconds),
`finishCounter`, `lastImprovedAt`.

The world record is rank 1. The overlay does not need a separate WR endpoint.

### `GET /leaderboard`

Paged event leaderboard. Query: `eventId`, `limit`, `offset`.

Use this only if adding an event standings widget.

### `GET /supporters/top-donors`

Query: `days` (default 90), `limit`.

Fields: `rank`, `name` (null for anonymous), `amount` (EUR), `tier` (null for no tier).

A row with a null name renders as `Anonymous` and keeps the amount.

### `GET /streamers/live`

Returns the live streamer snapshot. Fields include `liveStatus` (`fresh`, `stale`,
`unavailable`) and the streamer list.

Only `fresh` is current. A `stale` or `unavailable` answer may carry an earlier snapshot.

## CORS

The API allows a fixed origin list. The overlay origin must be added for the deployed host.
Local development on `http://localhost:5173` may already be allowed.

If adding the origin is not possible, use a small Cloudflare Pages Function that proxies the
same paths.

## Polling & Rate Limits

The public API does not currently enforce a rigid rate limit, but client apps must poll responsibly:
- Aim for 20–60 second poll intervals depending on the widget.
- Back off exponentially on repeated network errors or 5xx responses.
- Pause polling when the document or tab is hidden.
