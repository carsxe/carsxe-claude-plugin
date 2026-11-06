---
description: Retrieve a vehicle history report from a VIN via the CarsXE MCP server.
---

# CarsXE — Vehicle History

Retrieve the history report for a vehicle using the VIN provided in $ARGUMENTS via `get_vehicle_history`.

## Steps

1. Parse $ARGUMENTS to extract the VIN.
2. If no VIN is provided, ask: "Please provide a VIN to look up the vehicle history."
3. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
4. Call `get_vehicle_history` with `{ "vin": "<VIN>" }`. Include `format` only if the user asked for a specific format (`json` or `xml`).
5. Present the history report clearly:
   - Ownership history (number of owners, states)
   - Accident / damage records
   - Title status (clean, salvage, rebuilt, etc.)
   - Odometer readings over time
   - Service & maintenance records (if available)
   - Theft records
6. Flag any red flags prominently (e.g., salvage title, multiple accidents).
7. Handle errors gracefully.
