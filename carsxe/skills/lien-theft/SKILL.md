---
name: lien-theft
description: Check for active liens and theft records on a vehicle by VIN using the CarsXE MCP server. Use this when a user asks whether a car has a lien, is stolen, or wants to verify ownership is clean before buying.
---

When the user asks about liens, theft status, or ownership encumbrances on a vehicle:

1. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
2. Call `check_lien_and_theft` with `{ "vin": "<VIN>" }`.
3. Present the lien status and theft records clearly.
4. Highlight any active liens or theft flags prominently — these are critical red flags for buyers.
5. If the connector is not signed in, tell the user to run `/carsxe:auth` and sign in with their CarsXE account.
