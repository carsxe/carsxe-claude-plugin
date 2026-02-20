# CarsXE — Lien & Theft Check

Check for active liens and theft records on a vehicle using the VIN provided in $ARGUMENTS.

## Steps

1. Parse $ARGUMENTS to extract the VIN (required).
2. If no VIN is provided, ask: "Please provide a VIN to check for liens and theft records (e.g., `/carsxe:lien WBAFR7C57CC811956`)."
3. Make an HTTP GET request:
   ```
   GET https://api.carsxe.com/v1/lien-theft?key=<CARSXE_API_KEY>&vin=<VIN>
   ```
   Replace `<CARSXE_API_KEY>` with the value of the environment variable `CARSXE_API_KEY`.
4. Present the results clearly:
   - Active lien status (yes/no)
   - Lien holder details if applicable
   - Theft record status (stolen / not stolen)
   - Any related dates or jurisdiction info
5. Highlight any active liens or theft records prominently as they are critical for buyers.
6. Handle errors gracefully (invalid VIN, no data, auth error).
