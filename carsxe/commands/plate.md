---
description: Look up a vehicle from a license plate via the CarsXE MCP server.
---

# CarsXE — License Plate Decoder

Decode the license plate provided in $ARGUMENTS using the CarsXE MCP tool `decode_license_plate`.

## Steps

1. Parse $ARGUMENTS to extract:
   - `plate` (required): the license plate number
   - `country` (optional, default `US`): 2-letter country code (e.g., `US`, `GB`, `DE`)
   - `state` (optional): 2-letter US state code (e.g., `CA`) — recommended for US plates
   - `district` (optional): district or region within the country, if the user supplied one

   Examples:
   - `/carsxe:plate 7XER187 US CA` → plate=7XER187, country=US, state=CA
   - `/carsxe:plate AB123CD GB` → plate=AB123CD, country=GB

2. If `plate` is missing, ask: "Please provide a plate number and country code (e.g., `/carsxe:plate 7XER187 US CA`)."

3. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.

4. Call `decode_license_plate` with `plate`, plus `country` and `state` when provided.

5. Present the results clearly:
   - Vehicle Make, Model, Year
   - VIN (if returned)
   - Registration details (if available)
   - Engine & trim info

6. Handle errors gracefully (plate not found, invalid country, not connected).
