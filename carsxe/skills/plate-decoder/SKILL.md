---
name: plate-decoder
description: Look up vehicle information from a license plate number using the CarsXE MCP server. Use this when a user mentions a license plate and wants to know what vehicle it belongs to.
---

When the user provides a license plate number:

1. Extract the following from the user's message:
   - `plate` (required): the license plate number — if not provided, alert the user:
     > "Please provide a license plate number."
   - `country` (optional, default `US`): ISO 3166-1 alpha-2 country code (e.g., `US`, `AU`, `GB`)
   - `state` (recommended for US plates): 2-letter state/province code (e.g., `CA`, `NY`) — if a US plate is given without a state, alert the user:
     > "Please provide a state code (e.g., CA, NY, TX)."

2. Do not call the tool until `plate` is provided (and `state` for US plates).

3. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.

4. Call `decode_license_plate` with `plate`, plus `country` and `state` when known.

5. Present the results: vehicle Make, Model, Year, VIN (if returned), and registration info.

6. If the connector is not signed in, tell the user to run `/carsxe:auth` and sign in with their CarsXE account.
