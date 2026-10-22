---
name: check-road-conditions
description: Check current NSW road hazards (incidents, roadworks, major events, floods, fires, alpine conditions) and confirm the Live Traffic feed is healthy, using the Live Traffic Hazards and Site Status APIs.
api: openapi/opendata-transport-nsw-gov-au-live-traffic-hazards-openapi.yml
operations:
  - GetOpenTrafficIncidents
  - GetOpenRoadwork
  - GetOpenMajorEvent
  - GetOpenFlood
  - GetOpenFire
  - GetOpenAlpine
generated: '2026-10-21'
method: generated
---
# Check road conditions (Live Traffic Hazards API)

Every call needs `Authorization: apikey <TOKEN>`. Responses are JSON (GeoJSON features).

1. **Confirm the feed is up**: `GetTrafficSiteStatus` (`GET /v1/live/status`, Live Traffic Site Status API, `openapi/opendata-transport-nsw-gov-au-live-traffic-site-status-openapi.yml`).
2. **Pull current hazards** from `https://api.transport.nsw.gov.au/v1/live/hazards`: `GetOpenTrafficIncidents` (`/incident/open`), `GetOpenRoadwork` (`/roadwork/open`), `GetOpenMajorEvent` (`/majorevent/open`), and by season `GetOpenFlood`, `GetOpenFire`, `GetOpenAlpine`.
3. Filter the features by geometry or road name client-side. Use the `/all` and `/closed` variants only when you need history.

Rules: GET reads only, safe to retry. `401` = bad key, `404` = wrong path, `500`/`503` = back off and retry.
