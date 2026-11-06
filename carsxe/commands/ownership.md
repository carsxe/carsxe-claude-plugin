---
description: Look up registered owners and residents (Enterprise) via the CarsXE MCP server.
---

# CarsXE — Ownership (Enterprise)

Look up registered owners and residents. Available on Enterprise plans only. All four lookups share the same `ownership` entitlement.

## Steps

1. Parse $ARGUMENTS to extract the lookup type as the first token:
   - `vin` — registered owner(s) by VIN → `get_ownership_by_vin`
   - `person` — person by name and address → `get_ownership_by_person`
   - `address` — residents at a street address → `get_ownership_by_address`
   - `zip` — people in a ZIP with optional filters → `get_ownership_by_zip`

   Do **not** call a phone-number ownership lookup — that is out of scope for this plugin.

2. If no lookup type is provided, ask: "Please provide a lookup type: `vin`, `person`, `address`, or `zip` (e.g., `/carsxe:ownership vin 1FT8X3BT0BEA61538`)."

3. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.

4. Shared optional param for all lookups:
   - `include` (optional): comma-separated subset of `demographics,emails,phones,vehicle_history`. Omit it to get everything. `include` only shapes which sections are shown; it does not change billing.

5. **vin**
   - Required: 17-character VIN
   - Example: `/carsxe:ownership vin 1FT8X3BT0BEA61538`
   - Call `get_ownership_by_vin` with `vin` and optional `include`.
   - Present vehicle attributes, then each owner: name, age, gender, address, first/last observed, contact info, demographics, and vehicle history.

6. **person**
   - Required: `firstName` (max 50), `lastName` (max 50), `address` (street only, no city/state, max 100), `zip` (5-digit US ZIP, optionally ZIP+4)
   - Example: `/carsxe:ownership person John Sample "123 Example St" 90210`
   - Call `get_ownership_by_person` with `firstName`, `lastName`, `address`, `zip`, and optional `include`.
   - Present `count` and each match (name, address, VIN, emails, phones, demographics, vehicle history).

7. **address**
   - Required: `address` (street only, max 100), `zip` (5-digit US ZIP, optionally ZIP+4)
   - Optional: `variant` (legacy alias: `vehicle_history` or `compliance`; prefer `include`)
   - Example: `/carsxe:ownership address "123 Example St" 90210`
   - Call `get_ownership_by_address` with `address`, `zip`, and optional `include` / `variant`.
   - Present each resident the same way as person matches.

8. **zip**
   - Required: `zip` (exactly 5-digit US ZIP)
   - Optional: `gender` (`M` or `F`), `minAge`, `maxAge`, `income` (code or label, e.g. `F` or `$50,000–$59,999`), `page` (default 1), `limit` (default 15, max 100), `include`, `variant` (legacy)
   - Example: `/carsxe:ownership zip 90210 gender=F min_age=45 page=1 limit=15`
   - Call `get_ownership_by_zip` with `zip` and the optional filters (`minAge` / `maxAge` in camelCase).
   - Present page, limit, record count, and each record. Offer the next page if a full page was returned.

9. Handle errors:
   - No match / `no_data` → nothing was billed. Say so clearly.
   - Entitlement error → this lookup is Enterprise-only; the connected account may not have access.
   - Invalid VIN, ZIP, or missing required fields → ask for the missing input.
   - Not connected → follow `/carsxe:auth`.

## Notes

- Billing is per returned record (`owners` / `matches` / `records`), not per request. ZIP can return many records — warn before using a high `limit`.
- Street `address` must not include city or state.
