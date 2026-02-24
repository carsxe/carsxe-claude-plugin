# CarsXE — Vehicle History

Retrieve the history report for a vehicle using the VIN provided in $ARGUMENTS.

## Steps

1. Parse $ARGUMENTS to extract the VIN.
2. If no VIN is provided, ask: "Please provide a VIN to look up the vehicle history."
3. Make an HTTP GET request:
   ```
   GET https://api.carsxe.com/history?key=CARSXE_API_KEY&vin={VIN}
   ```
   Replace `CARSXE_API_KEY` with the value of the environment variable `CARSXE_API_KEY`.
4. Present the history report clearly:
   - Ownership history (number of owners, states)
   - Accident / damage records
   - Title status (clean, salvage, rebuilt, etc.)
   - Odometer readings over time
   - Service & maintenance records (if available)
   - Theft records
5. Flag any red flags prominently (e.g., salvage title, multiple accidents).
6. Handle errors gracefully.
