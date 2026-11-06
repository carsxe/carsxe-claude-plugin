---
description: Estimate a vehicle's market value from a VIN via the CarsXE MCP server.
---

# CarsXE — Market Value

Get the current market value of a vehicle using the VIN provided in $ARGUMENTS via `get_market_value`.

## Steps

1. Parse $ARGUMENTS to extract the VIN (required).
2. If no VIN is provided, ask: "Please provide a VIN to get the market value (e.g., `/carsxe:value WBAFR7C57CC811956`)."
3. Parse $ARGUMENTS for optional parameters: `state` (US state code), `mileage` (numeric), `condition` (`excellent` / `clean` / `average` / `rough`).
4. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
5. Call `get_market_value` with `vin` and any optional `state`, `mileage`, and `condition`.
6. Present the results in a clear format:
   - Current estimated market value
   - Value range (low / average / high) if available
   - Historical value trend if available
   - Vehicle summary (year, make, model)
7. When the host supports MCP Apps UI, call `render_market_value` with the structured result from `get_market_value` (always fetch value first).
8. Handle errors gracefully (invalid VIN, no data found, not connected).
