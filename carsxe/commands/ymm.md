---
description: Look up vehicle data by year, make, and model via the CarsXE MCP server.
---

# CarsXE — Year / Make / Model Lookup

Look up vehicle data by Year, Make, and Model using `get_year_make_model`.

## Steps

1. Parse $ARGUMENTS to extract:
   - `year` (required): 4-digit year (e.g., 2020)
   - `make` (required): vehicle manufacturer (e.g., Toyota, Ford)
   - `model` (required): vehicle model (e.g., Camry, F-150)
   - `trim` (optional): specific trim level (e.g., LE, Sport, Limited)

   Example: `/carsxe:ymm 2020 Toyota Camry LE`

2. If `year`, `make`, or `model` are missing, ask: "Please provide year, make, and model (e.g., `/carsxe:ymm 2020 Toyota Camry`)."

3. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.

4. Call `get_year_make_model` with `year`, `make`, `model`, and `trim` only if the user specified it.

5. Present the results in a clean format:
   - Available trims (if not specified)
   - Engine options, transmission, drivetrain
   - Fuel type and economy
   - Body style and dimensions
   - Standard features

6. Handle errors gracefully (no data found, invalid params, not connected).

## Notes

- To list available years, makes, models, or variants first, use `/carsxe:ymm-options`.
