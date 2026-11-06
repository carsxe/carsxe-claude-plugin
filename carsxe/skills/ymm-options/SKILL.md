---
name: ymm-options
description: List year, make, model, trim, or variant options for cascading vehicle dropdowns using the CarsXE MCP server. Use this when the user wants available years, makes, models, trims, or which years a vehicle was sold — not full specs.
---

When the user wants to browse available years, makes, models, trims, or variants (dropdowns, "what years was X sold", "which models does Toyota have in 2023"):

1. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
2. Call `get_ymm_options` with only filters the user provided (`dimension`, `year`, `make`, `model`, `trim`).
   `dimension` is optional: `years` | `makes` | `models` | `trims` | `variants`.
3. If `dimension` is omitted, infer the next list: no filters → years; year → makes; make → models; make + model → variants.
4. Present the single returned list. Show `message` if present. For bulk variants (`dimension=variants` + year + make, no model), mention `modelCount` — that is the billed unit count — and warn before making that call.
5. Offer to fetch the next dropdown level or to run `get_year_make_model` for full specs of a chosen year/make/model.
6. If the connector is not signed in, tell the user to run `/carsxe:auth` and sign in with their CarsXE account.
