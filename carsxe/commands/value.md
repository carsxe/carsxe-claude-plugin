# CarsXE — Market Value

Get the current market value of a vehicle using the VIN provided in $ARGUMENTS.

## Steps

1. Parse $ARGUMENTS to extract the VIN (required).
2. If no VIN is provided, ask: "Please provide a VIN to get the market value (e.g., `/carsxe:value WBAFR7C57CC811956`)."
3. Make an HTTP GET request:
   ```
   GET https://api.carsxe.com/v2/marketvalue?key=<CARSXE_API_KEY>&vin=<VIN>
   ```
   Replace `<CARSXE_API_KEY>` with the value of the environment variable `CARSXE_API_KEY`.
4. Present the results in a clear format:
   - Current estimated market value
   - Value range (low / average / high) if available
   - Historical value trend if available
   - Vehicle summary (year, make, model)
5. Handle errors gracefully (invalid VIN, no data found, auth error).
