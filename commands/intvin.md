# CarsXE — International VIN Decoder

Decode an international VIN provided in $ARGUMENTS using the CarsXE International VIN Decoder API.

## Steps

1. Parse $ARGUMENTS to extract the VIN (required).
2. If no VIN is provided, ask: "Please provide an international VIN to decode (e.g., `/carsxe:intvin WF0MXXGBWM8R43240`)."
3. Make an HTTP GET request:
   ```
   GET https://api.carsxe.com/v1/international-vin-decoder?key=<CARSXE_API_KEY>&vin=<VIN>
   ```
   Replace `<CARSXE_API_KEY>` with the value of the environment variable `CARSXE_API_KEY`.
4. Present the decoded information:
   - Country of manufacture
   - Make, Model, Year
   - Engine & transmission details
   - Body style
   - Any other returned attributes
5. Note: this endpoint is optimized for non-US VINs (European, Asian manufacturers, etc.).
6. Handle errors gracefully.
