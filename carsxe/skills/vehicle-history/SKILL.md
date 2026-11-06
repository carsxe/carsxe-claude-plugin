---
name: vehicle-history
description: Retrieve a vehicle history report from a VIN using the CarsXE MCP server. Use this when a user wants to know a car's history — past owners, accidents, title status, odometer readings, or whether it's been in a crash.
---

When the user asks about a vehicle's history, past accidents, title status, or ownership:

1. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
2. Call `get_vehicle_history` with `{ "vin": "<VIN>" }`.
3. Summarize the history report:
   - Number of previous owners
   - Accident / damage records
   - Title status (clean, salvage, rebuilt, lemon)
   - Odometer history
   - Theft records
4. Clearly highlight any red flags (salvage title, accidents, odometer rollback).
5. If the connector is not signed in, tell the user to run `/carsxe:auth` and sign in with their CarsXE account.
