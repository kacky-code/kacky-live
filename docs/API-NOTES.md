# API notes

The overlay reads the public KackyGG API. All paths below are under `/v1`.

| Environment | Base URL |
|---|---|
| Production | `https://api.kacky.gg/v1` |
| Development | `https://api-dev.kacky.gg/v1` |

## Rules

- Anonymous `GET` only. No writes, no auth, no cookies.
- Do not scrape the website. Use these endpoints.
- Do not call the OpenAPI document in production. It is not served there.
- Poll politely. The intervals in the overlay spec are the starting point.
- The API returns `{ data, meta }` for paged endpoints, not a bare array.
- A missing or private server answers `404`. Treat it as "hide the widget", not as an error.
- `GET /events/active` answers `404` when no event is running.

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

Use this only if the spec adds an event standings widget.

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
Local development on `http://localhost:5173` may already be allowed for another app. Confirm
before relying on it.

If adding the origin is not possible, use a small Cloudflare Pages Function that proxies the
same paths. Do not put an API key in the client.

## Rate limits

There is no public rate limit for these endpoints today. Do not treat that as permission to poll
every second. One overlay per streamer, 20 to 60 second polls, and backoff on errors.
