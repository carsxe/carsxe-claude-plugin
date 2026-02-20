# CarsXE — Vehicle Recalls

Check for active recalls on a vehicle using the VIN provided in $ARGUMENTS.

## Steps

1. Parse $ARGUMENTS to extract the VIN (required).
2. If no VIN is provided, ask: "Please provide a VIN to check for recalls (e.g., `/carsxe:recalls WBAFR7C57CC811956`)."
3. Make an HTTP GET request:
   ```
   GET https://api.carsxe.com/v1/recalls?key=<CARSXE_API_KEY>&vin=<VIN>
   ```
   Replace `<CARSXE_API_KEY>` with the value of the environment variable `CARSXE_API_KEY`.
4. Present recall information clearly:
   - Number of open recalls
   - For each recall: campaign number, component affected, description of defect, remedy available, date
   - Whether each recall has been remedied
5. If no recalls are found, clearly confirm the vehicle has no open recalls.
6. Handle errors gracefully.
