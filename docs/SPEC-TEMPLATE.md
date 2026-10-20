# Overlay Spec Template

Use this template to propose a layout or widget spec before implementing. Keep it concise (1–2 pages) and include a mockup or wireframe.

## 1. Context & Surface

- **Target Surface:** OBS browser source (1920x1080 transparent), Twitch panel, or both.
- **Use Case:** Streamer overlay during live hunting, tournament broadcast, etc.

## 2. URL Parameters

List query parameters, defaults, and validation rules.

```text
/overlay?server=<server-login>&player=<player-login>&theme=<theme-id>
```

## 3. Data & Polling

| Widget | Endpoint | Key Fields | Suggested Poll |
|---|---|---|---|
| Event header | `GET /v1/events/active` | `name`, `edition`, `startTime`, `endTime` | 60 s |
| Current map | `GET /v1/servers/{login}/maps` | `currentMap` | 20 s |
| Map detail | `GET /v1/maps/{number}` | `name`, `authorTime`, `imageUrl`, `totalFinishers` | On map change |
| Top 5 records | `GET /v1/maps/{number}/records?limit=5` | `rank`, `nickname`, `score` | 20 s |
| Server queue | `GET /v1/servers/{login}/maps` | `nextMaps` | 20 s |
| Top donors | `GET /v1/supporters/top-donors?days=90&limit=5` | `rank`, `name`, `amount` | 60 s |

## 4. Layout & Visuals

Attach a mockup image or ASCII wireframe. Describe positioning, typography hierarchy, and contrast for Trackmania backdrops.

## 5. UI States & Fallbacks

For each widget, specify:
- **Loading:** Skeleton placeholder or transparent space.
- **Error / Offline:** Hold last known state; do not show error popups or stack traces on stream.
- **Empty:** Clean empty state or hidden widget.
- **Overflow:** Truncation rule for long map or player names.

## 6. Acceptance & Testing

Key sanity checks to verify the implementation:
- Renders cleanly in OBS browser source at 1920x1080 without scrollbars.
- Holds last good state across network timeouts.
- Player nicknames strip Trackmania style/color codes (`$f00`, `$i`, etc.).
- Performance stays light with zero impact on stream frame rates.
