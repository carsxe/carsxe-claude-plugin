# CarsXE — Year / Make / Model Lookup

Look up vehicle data by Year, Make, and Model using the CarsXE YMM API.

## Steps

1. Parse $ARGUMENTS to extract:
   - `year` (required): 4-digit year (e.g., 2020)
   - `make` (required): vehicle manufacturer (e.g., Toyota, Ford)
   - `model` (required): vehicle model (e.g., Camry, F-150)
   - `trim` (optional): specific trim level (e.g., LE, Sport, Limited)

   Example: `/carsxe:ymm 2020 Toyota Camry LE`

2. If `year`, `make`, or `model` are missing, ask: "Please provide year, make, and model (e.g., `/carsxe:ymm 2020 Toyota Camry`)."

3. Make an HTTP GET request:

   ```
   GET https://api.carsxe.com/v1/ymm?key=<CARSXE_API_KEY>&year=<YEAR>&make=<MAKE>&model=<MODEL>[&trim=<TRIM>]
   ```

   Replace `<CARSXE_API_KEY>` with the value of the environment variable `CARSXE_API_KEY`. Only include `trim` if the user specified it.

4. Present the results in a clean format:
   - Available trims (if not specified)
   - Engine options, transmission, drivetrain
   - Fuel type and economy
   - Body style and dimensions
   - Standard features

5. Handle errors gracefully (no data found, invalid params, auth error).
