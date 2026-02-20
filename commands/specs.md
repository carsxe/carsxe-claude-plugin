# CarsXE — Vehicle Specifications (VIN Decoder)

Decode the VIN provided in $ARGUMENTS using the CarsXE Specifications API.

## Steps

1. Parse $ARGUMENTS to extract:
   - `vin` (required): 17-character alphanumeric string
   - `deepdata` (optional): pass `"true"` to get extended data
   - `disableIntVINDecoding` (optional): pass `"true"` to disable international VIN decoding fallback

2. If no VIN is provided, ask: "Please provide a VIN to decode (e.g., `/carsxe:specs WBAFR7C57CC811956`)."

3. Make an HTTP GET request:

   ```
   GET https://api.carsxe.com/specs?key=<CARSXE_API_KEY>&vin=<VIN>[&deepdata=true][&disableIntVINDecoding=true]
   ```

   Replace `<CARSXE_API_KEY>` with the value of the environment variable `CARSXE_API_KEY`.

4. Present the response in a clean, readable format including:
   - Make, Model, Year, Trim
   - Engine details (type, cylinders, displacement, horsepower)
   - Transmission & drivetrain
   - Fuel type & economy
   - Body style & dimensions
   - Equipment & features (if available)

5. Handle errors gracefully (invalid VIN, missing API key, etc.).

## Notes

- A valid VIN is exactly 17 characters (letters and numbers, no I, O, or Q).
- Remind the user to set the `CARSXE_API_KEY` environment variable if auth fails.
