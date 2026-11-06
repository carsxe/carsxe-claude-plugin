---
name: ownership
description: Look up registered vehicle owners and residents using CarsXE ownership tools (Enterprise). Use this when the user asks who owns a VIN, who lives at an address, contact details for a named person, or people in a ZIP. Do not use for lien/theft checks.
---

When the user asks who owns a vehicle, who lives at an address, contact details for a person, or people in a ZIP (Enterprise only):

If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.

1. Choose one lookup. Do **not** run a phone-number ownership lookup.
   - VIN → `get_ownership_by_vin` with `vin` and optional `include`
   - Person → `get_ownership_by_person` with `firstName`, `lastName`, `address`, `zip`, and optional `include`
   - Address → `get_ownership_by_address` with `address`, `zip`, and optional `include`
   - ZIP → `get_ownership_by_zip` with `zip` and optional `gender`, `minAge`, `maxAge`, `income`, `page`, `limit`, `include`
2. `include` is optional: comma-separated `demographics,emails,phones,vehicle_history`. Omit it to get everything.
3. Street `address` is street only — no city or state. ZIP is 5-digit US (person/address may be ZIP+4; zip lookup is exactly 5 digits).
4. Present matches clearly (name, address, contact, demographics, linked vehicles). No match / `no_data` is not billed.
5. Billing is per returned record. Warn before a ZIP search with a high `limit` (default 15, max 100).
6. If the connected account lacks entitlement, say this lookup is Enterprise-only. If the connector is not signed in, tell the user to run `/carsxe:auth`.
