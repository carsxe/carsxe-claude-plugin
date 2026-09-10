# CarsXE — Recalls by Year / Make / Model

Check safety recalls for a model line using year, make, and model — no VIN required.

## Steps

1. Parse $ARGUMENTS to extract:
   - `year` (required): 4-digit model year (e.g. 2023). Must be between 1900 and the current model year plus one.
   - `make` (required): vehicle manufacturer (e.g. Toyota)
   - `model` (required): vehicle model (e.g. Camry)

   Example: `/carsxe:recalls-ymm 2023 Toyota Camry`

2. If `year`, `make`, or `model` are missing, ask: "Please provide year, make, and model (e.g., `/carsxe:recalls-ymm 2023 Toyota Camry`)."

3. Make an HTTP GET request:

   ```
   GET https://api.carsxe.com/v1/recalls-ymm?key=<CARSXE_API_KEY>&year=<YEAR>&make=<MAKE>&model=<MODEL>&source=claude_plugin
   ```

   Replace `<CARSXE_API_KEY>` with the value of the environment variable `CARSXE_API_KEY`.

4. Present recall information clearly:
   - Year, make, and model (normalized)
   - Number of recalls (`recall_count`) and whether any exist (`has_recalls`)
   - For each recall: NHTSA campaign number, manufacturer, component, summary, consequence, remedy, report date
   - Highlight `park_it`, `park_outside`, or over-the-air remedy flags when true

5. If no recalls are found, clearly confirm the model line has no safety recalls.

6. Handle errors gracefully (invalid year/make/model, no data, auth error).

## Notes

- This is a model-line search, not a specific vehicle. For a single VIN use `/carsxe:recalls`.
- For many VINs at once use `/carsxe:recalls-batch`.
