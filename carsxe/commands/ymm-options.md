# CarsXE — Year / Make / Model Options

List years, makes, models, trims, or variants for cascading dropdowns using the CarsXE YMM Options API.

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

2. Make an HTTP GET request. Include only the filters the user provided:

   ```
   GET https://api.carsxe.com/v1/ymm-options?key=<CARSXE_API_KEY>&source=claude_plugin[&dimension=<DIMENSION>][&year=<YEAR>][&make=<MAKE>][&model=<MODEL>][&trim=<TRIM>]
   ```

   Replace `<CARSXE_API_KEY>` with the value of the environment variable `CARSXE_API_KEY`.

3. When `dimension` is omitted, the API returns one inferred list:

   | make | model | year | Returns |
   | ---- | ----- | ---- | ------- |
   | — | — | — | `years` |
   | — | — | ✓ | `makes` |
   | ✓ | — | * | `models` |
   | ✓ | ✓ | * | `variants` |

4. Present the returned list (`years`, `makes`, `models`, `trims`, or `variants`) as a clean bullet list. If `message` is present, show it. If `modelCount` is present (bulk variants), mention it — that value is the billed unit count.

5. Handle errors gracefully (missing required filters, ambiguous model name, auth error).

## Notes

- One list per request. To populate the next dropdown, call again with the extra filter.
- Bulk variants (`dimension=variants` + `year` + `make`, no `model`) bills 1 unit per model (`modelCount`). Warn the user before making that call.
- For full specs of a chosen year/make/model use `/carsxe:ymm`.
