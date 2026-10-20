# Overlay spec

Fill this in before writing code. Keep it to one page. Attach one mockup image.

## 1. User and channel

Who is the streamer? Which channel and language? What does their overlay look like today?

## 2. Surface

OBS browser source, Twitch panel extension, or both? Which resolution and safe area?

## 3. URL

List every query parameter, its default and its validation rule.

```
/overlay?server=...&player=...&theme=...
```

## 4. Data

| Widget | Endpoint | Fields | Poll |
|---|---|---|---|
| Event header | `GET /v1/events/active` | `name`, `edition`, `startTime`, `endTime` | 60 s |
| Current map | `GET /v1/servers/{login}/maps` | `currentMap` | 20 s |
| Map detail | `GET /v1/maps/{number}` | `name`, `authorTime`, `imageUrl`, `totalFinishers` | on map change |
| Top 5 | `GET /v1/maps/{number}/records?limit=5` | `rank`, `nickname`, `score` | 20 s |
| Next maps | `GET /v1/servers/{login}/maps` | `nextMaps` | 20 s |
| Top donors | `GET /v1/supporters/top-donors?days=90&limit=5` | `rank`, `name`, `amount` | 60 s |

Add or remove rows to match the mockup.

## 5. Layout

Describe each block: position, size, type level, colour. One mockup image is enough.

## 6. States

For each widget, write what shows when:

- the first request is loading,
- the request fails,
- the response is empty,
- the value is too long.

## 7. Configuration

What can the streamer change? URL only, or a config page? Which values are validated?

## 8. Acceptance

Write the checks a reviewer will run. Example:

- The overlay renders the current KR7 map within 20 seconds of opening.
- Killing the API for 5 minutes leaves the last map and top 5 on screen.
- A map name longer than 40 characters truncates without moving the layout.
- The streamer can build the URL from the config page in under 5 minutes.

## 9. Non-goals

List what this version will not do.

## 10. Open questions

List the decisions that need a maintainer.
