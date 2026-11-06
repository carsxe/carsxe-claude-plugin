---
name: international-vin
description: Decode an international (non-US) VIN using the CarsXE MCP server. Use this when a user provides a VIN from a European, Asian, or other non-US vehicle and wants to decode it.
---

When the user provides a VIN that appears to be from a non-US vehicle (European, Asian, etc.):

1. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
2. Call `decode_international_vin` with `{ "vin": "<VIN>" }`.
3. Present the decoded data: country of manufacture, make, model, year, engine, transmission, body style.
4. Note this lookup is optimized for international VINs outside the US market.
5. If the connector is not signed in, tell the user to run `/carsxe:auth` and sign in with their CarsXE account.
