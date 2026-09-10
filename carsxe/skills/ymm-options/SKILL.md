---
name: ymm-options
description: List year, make, model, trim, or variant options for cascading vehicle dropdowns using the CarsXE YMM Options API. Use this when the user wants available years, makes, models, trims, or which years a vehicle was sold — not full specs.
---

When the user wants to browse available years, makes, models, trims, or variants (dropdowns, "what years was X sold", "which models does Toyota have in 2023"):

1. Call the CarsXE YMM Options API. Include only filters the user provided:
   ```
   GET https://api.carsxe.com/v1/ymm-options?key={CARSXE_API_KEY}&source=claude_plugin[&dimension={DIMENSION}][&year={YEAR}][&make={MAKE}][&model={MODEL}][&trim={TRIM}]
   ```
   `dimension` is optional: `years` | `makes` | `models` | `trims` | `variants`.
2. If `dimension` is omitted, infer the next list: no filters → years; year → makes; make → models; make + model → variants.
3. Present the single returned list. Show `message` if present. For bulk variants (`dimension=variants` + year + make, no model), mention `modelCount` — that is the billed unit count — and warn before making that call.
4. Offer to fetch the next dropdown level or to run `/v1/ymm` for full specs of a chosen year/make/model.
5. If the API key is missing, tell the user to set the `CARSXE_API_KEY` environment variable.
