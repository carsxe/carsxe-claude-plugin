---
description: List year, make, model, trim, or variant options via the CarsXE MCP server.
---

# CarsXE — Year / Make / Model Options

List years, makes, models, trims, or variants for cascading dropdowns using `get_ymm_options`.

## Steps

1. Parse $ARGUMENTS to extract optional filters:
   - `dimension` (optional): `years` | `makes` | `models` | `trims` | `variants`
   - `year` (optional): 4-digit model year
   - `make` (optional): manufacturer (required for `dimension=models`)
   - `model` (optional): model name (required for `dimension=trims`; required for `dimension=variants` unless both `year` and `make` are set)
   - `trim` (optional): substring filter on trim or variant names (ignored for years/makes/models)

   Examples:
   - `/carsxe:ymm-options` → list years
   - `/carsxe:ymm-options 2023` → makes for 2023
   - `/carsxe:ymm-options 2023 Toyota` → models for 2023 Toyota
   - `/carsxe:ymm-options 2023 Toyota Camry` → variants
   - `/carsxe:ymm-options dimension=variants year=2025 make=Lexus`

2. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.

3. Call `get_ymm_options` with only the filters the user provided (`dimension`, `year`, `make`, `model`, `trim`).

4. When `dimension` is omitted, the tool returns one inferred list:

   | make | model | year | Returns |
   | ---- | ----- | ---- | ------- |
   | — | — | — | `years` |
   | — | — | ✓ | `makes` |
   | ✓ | — | * | `models` |
   | ✓ | ✓ | * | `variants` |

5. Present the returned list (`years`, `makes`, `models`, `trims`, or `variants`) as a clean bullet list. If `message` is present, show it. If `modelCount` is present (bulk variants), mention it — that value is the billed unit count.

6. Handle errors gracefully (missing required filters, ambiguous model name, not connected).

## Notes

- One list per request. To populate the next dropdown, call again with the extra filter.
- Bulk variants (`dimension=variants` + `year` + `make`, no `model`) bills 1 unit per model (`modelCount`). Warn the user before making that call.
- For full specs of a chosen year/make/model use `/carsxe:ymm`.
