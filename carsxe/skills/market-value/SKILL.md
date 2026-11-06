---
name: market-value
description: Get the current market value of a vehicle from its VIN using the CarsXE MCP server. Use this when a user asks how much a car is worth, wants to know its value, or is thinking about buying/selling a vehicle.
---

When the user asks about a vehicle's price, worth, or market value and has a VIN:

1. Ask if they want to provide optional parameters to refine the estimate:
   - `state` — US state code (e.g., `CA`, `TX`) for regional pricing
   - `mileage` — current mileage to adjust the value
   - `condition` — vehicle condition: `excellent`, `clean`, `average`, or `rough`
2. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
3. Call `get_market_value` with `vin` and any optional `state`, `mileage`, and `condition`.
4. Present the estimated market value clearly, including:
   - Current value estimate
   - Low / average / high range if available
   - Historical trend if available
5. Provide helpful context (e.g., whether the value is strong for its age/mileage if that info is available).
6. When the host supports MCP Apps UI, call `render_market_value` with the structured result (always fetch value first).
7. If the connector is not signed in, tell the user to run `/carsxe:auth` and sign in with their CarsXE account.
