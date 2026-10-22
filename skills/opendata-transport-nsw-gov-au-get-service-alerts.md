---
name: get-service-alerts
description: Fetch GTFS-realtime service alerts for all operators or a single mode (buses, ferries, light rail, metro, trains) from the Transport for NSW Realtime Alerts v2 API.
api: openapi/opendata-transport-nsw-gov-au-gtfs-realtime-alerts-v2-openapi.yml
operations:
  - GetAll
  - GetBuses
  - GetFerries
  - GetLightRail
  - Metro
  - GetNSWTrains
  - RegionBuses
  - SydneyTrains
generated: '2026-10-21'
method: generated
---
# Get service alerts (GTFS-realtime Alerts v2)

Base URL `https://api.transport.nsw.gov.au/v2/gtfs/alerts`. Every call needs `Authorization: apikey <TOKEN>`. Responses are `application/x-google-protobuf` (GTFS-realtime FeedMessage). Decode them with a GTFS-realtime protobuf binding. The TfNSW extension .proto is saved in `grpc/`.

1. **All operators**: `GetAll` (`GET /all`).
2. **One mode**: `GetBuses` (`/buses`), `GetFerries` (`/ferries`), `GetLightRail` (`/lightrail`), `Metro` (`/metro`), `GetNSWTrains` (`/nswtrains`), `RegionBuses` (`/regionbuses`), `SydneyTrains` (`/sydneytrains`).
3. Read `entity[].alert` for the affected routes and stops, the active periods and the header and description text.

Rules: GET reads only, safe to poll and retry. `401` = bad key.
