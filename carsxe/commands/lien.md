---
description: Check liens and theft records for a VIN via the CarsXE MCP server.
---

# CarsXE — Lien & Theft Check

Check for active liens and theft records on a vehicle using the VIN provided in $ARGUMENTS via `check_lien_and_theft`.

## Steps

1. Parse $ARGUMENTS to extract the VIN (required).
2. If no VIN is provided, ask: "Please provide a VIN to check for liens and theft records (e.g., `/carsxe:lien WBAFR7C57CC811956`)."
3. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
4. Call `check_lien_and_theft` with `{ "vin": "<VIN>" }`.
5. Present the results clearly:
   - Active lien status (yes/no)
   - Lien holder details if applicable
   - Theft record status (stolen / not stolen)
   - Any related dates or jurisdiction info
6. Highlight any active liens or theft records prominently as they are critical for buyers.
7. Handle errors gracefully (invalid VIN, no data, not connected).
