---
name: calculate-toll-cost
description: Get NSW toll road pricing and calculate the toll cost of a route with the Transport for NSW Toll Calculator API v2.
api: openapi/opendata-transport-nsw-gov-au-toll-calculator-v2-openapi.yml
operations:
  - getData
  - getRoutes
  - getMatch
generated: '2026-10-21'
method: generated
---
# Calculate a toll cost (Toll Calculator API v2)

Base URL `https://api.transport.nsw.gov.au/v2/roads`. Every call needs `Authorization: apikey <TOKEN>`.

1. **Reference data** (optional): `getData` (`GET /toll_calc/data`) returns toll road pricing information.
2. **From an origin and destination**: `getRoutes` (`POST /toll_calc/route`) with the required JSON `body` returns possible routes and their toll costs.
3. **From your own route**: `getMatch` (`POST /toll_calc/match`) with the required JSON `body` returns the toll cost breakdown for the route you supply.

Rules: the POSTs are calculations and change no state, but the contract makes no idempotency guarantee. Responses `400` (bad body), `401`/`403` (key), `404`. The v1 `/toll_calc` endpoint is deprecated, so use v2.
