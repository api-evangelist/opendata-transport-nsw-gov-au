---
name: plan-public-transport-trip
description: Resolve stops by name, plan a NSW public transport journey between them, and read live departures from a stop using the Transport for NSW Trip Planner API.
api: openapi/opendata-transport-nsw-gov-au-trip-planner-openapi.yml
operations:
  - tfnsw_stopfinder_request
  - tfnsw_trip_request2
  - tfnsw_dm_request
  - tfnsw_addinfo_request
generated: '2026-10-21'
method: generated
---
# Plan a public transport trip (Trip Planner API)

Base URL `https://api.transport.nsw.gov.au/v1/tp`. Every call needs the header `Authorization: apikey <TOKEN>` (Open Data Hub key).

1. **Find the stops**: `tfnsw_stopfinder_request` (`GET /stop_finder`). Required: `outputFormat=rapidJSON`, `type_sf` (e.g. `any` or `stop`), `name_sf` (free text or stop ID), `coordOutputFormat=EPSG:4326`. Take the stop `id` from the results for origin and destination.
2. **Plan the journey**: `tfnsw_trip_request2` (`GET /trip`). Required: `outputFormat`, `coordOutputFormat`, `depArrMacro` (`dep` or `arr`), `type_origin`/`name_origin`, `type_destination`/`name_destination` (use the stop IDs from step 1).
3. **Live departures** (optional): `tfnsw_dm_request` (`GET /departure_mon`). Required: `outputFormat`, `coordOutputFormat`, `type_dm=stop`, `name_dm=<stop id>`.
4. **Disruptions** (optional): `tfnsw_addinfo_request` (`GET /add_info`), with `outputFormat` required, for service alerts that affect the planned legs.

Rules: all operations are GET reads and safe to retry. `401` means the key is missing or malformed (it must be prefixed with `apikey `). For `500`/`503`, back off and retry.
