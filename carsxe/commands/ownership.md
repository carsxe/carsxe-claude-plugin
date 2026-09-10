# CarsXE — Ownership (Enterprise)

Look up registered owners and residents. Available on Enterprise plans only. All four lookups share the same `ownership` entitlement.

## Steps

1. Parse $ARGUMENTS to extract the lookup type as the first token:
   - `vin` — registered owner(s) by VIN
   - `person` — person by name and address
   - `address` — residents at a street address
   - `zip` — people in a ZIP with optional filters

   Do **not** call `/v1/ownership/phone` — that endpoint is out of scope for this plugin.

2. If no lookup type is provided, ask: "Please provide a lookup type: `vin`, `person`, `address`, or `zip` (e.g., `/carsxe:ownership vin 1FT8X3BT0BEA61538`)."

3. Shared optional param for all lookups:
   - `include` (optional): comma-separated subset of `demographics,emails,phones,vehicle_history`. Omit it to get everything. `include` only shapes which sections are shown; it does not change billing.

4. **vin**
   - Required: 17-character VIN
   - Example: `/carsxe:ownership vin 1FT8X3BT0BEA61538`
   - ```
     GET https://api.carsxe.com/v1/ownership/vin?key=<CARSXE_API_KEY>&vin=<VIN>&source=claude_plugin[&include=<INCLUDE>]
     ```
   - Present vehicle attributes, then each owner: name, age, gender, address, first/last observed, contact info, demographics, and vehicle history.

5. **person**
   - Required: `first_name` (max 50), `last_name` (max 50), `address` (street only, no city/state, max 100), `zip` (5-digit US ZIP, optionally ZIP+4)
   - Example: `/carsxe:ownership person John Sample "123 Example St" 90210`
   - ```
     GET https://api.carsxe.com/v1/ownership/person?key=<CARSXE_API_KEY>&first_name=<FIRST>&last_name=<LAST>&address=<ADDRESS>&zip=<ZIP>&source=claude_plugin[&include=<INCLUDE>]
     ```
   - Present `count` and each match (name, address, VIN, emails, phones, demographics, vehicle history).

6. **address**
   - Required: `address` (street only, max 100), `zip` (5-digit US ZIP, optionally ZIP+4)
   - Optional: `variant` (legacy alias: `vehicle_history` or `compliance`; prefer `include`)
   - Example: `/carsxe:ownership address "123 Example St" 90210`
   - ```
     GET https://api.carsxe.com/v1/ownership/address?key=<CARSXE_API_KEY>&address=<ADDRESS>&zip=<ZIP>&source=claude_plugin[&include=<INCLUDE>][&variant=<VARIANT>]
     ```
   - Present each resident the same way as person matches.

7. **zip**
   - Required: `zip` (exactly 5-digit US ZIP)
   - Optional: `gender` (`M` or `F`), `min_age`, `max_age`, `income` (code or label, e.g. `F` or `$50,000–$59,999`), `page` (default 1), `limit` (default 15, max 100), `include`, `variant` (legacy)
   - Example: `/carsxe:ownership zip 90210 gender=F min_age=45 page=1 limit=15`
   - ```
     GET https://api.carsxe.com/v1/ownership/zip?key=<CARSXE_API_KEY>&zip=<ZIP>&source=claude_plugin[&gender=<GENDER>][&min_age=<MIN>][&max_age=<MAX>][&income=<INCOME>][&page=<PAGE>][&limit=<LIMIT>][&include=<INCLUDE>][&variant=<VARIANT>]
     ```
   - Present page, limit, record count, and each record. Offer the next page if a full page was returned.

8. Replace `<CARSXE_API_KEY>` with the value of the environment variable `CARSXE_API_KEY`.

9. Handle errors:
   - HTTP 404 / `error: "no_data"` → no match; nothing was billed. Say so clearly.
   - HTTP 401 / entitlement error → this API is Enterprise-only; the user's key may not have access.
   - Invalid VIN, ZIP, or missing required fields → ask for the missing input.

## Notes

- Billing is per returned record (`owners` / `matches` / `records`), not per request. ZIP can return many records — warn before using a high `limit`.
- Street `address` must not include city or state.
