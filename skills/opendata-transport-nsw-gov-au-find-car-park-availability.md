---
name: find-car-park-availability
description: List Transport for NSW car parks, read real-time occupancy for a facility, and pull its occupancy history with the Car Park API.
api: openapi/opendata-transport-nsw-gov-au-car-park-openapi.yml
operations:
  - GetCarParkFull-list
  - GetCarPark
  - GetCarParkHistory
generated: '2026-10-21'
method: generated
---
# Find car park availability (Car Park API)

Base URL `https://api.transport.nsw.gov.au/v1`. Every call needs `Authorization: apikey <TOKEN>`.

1. **List facilities**: `GetCarParkFull-list` (`GET /carpark/full-list`) returns facility IDs and names.
2. **Real-time occupancy**: `GetCarPark` (`GET /carpark`), with an optional facility query parameter.
3. **History**: `GetCarParkHistory` (`GET /carpark/history`). Required: `facility` and `eventdate`.

Rules: GET reads only, safe to retry. `401` = bad key, `404` = unknown facility or path, `500`/`503` = back off.
