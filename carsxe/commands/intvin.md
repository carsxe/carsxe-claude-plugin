---
description: Decode an international (non-US) VIN via the CarsXE MCP server.
---

# CarsXE — International VIN Decoder

Decode an international VIN provided in $ARGUMENTS using `decode_international_vin`.

## Steps

1. Parse $ARGUMENTS to extract the VIN (required).
2. If no VIN is provided, ask: "Please provide an international VIN to decode (e.g., `/carsxe:intvin WF0MXXGBWM8R43240`)."
3. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
4. Call `decode_international_vin` with `{ "vin": "<VIN>" }`.
5. Present the decoded information:
   - Country of manufacture
   - Make, Model, Year
   - Engine & transmission details
   - Body style
   - Any other returned attributes
6. Note: this lookup is optimized for non-US VINs (European, Asian manufacturers, etc.).
7. Handle errors gracefully.
