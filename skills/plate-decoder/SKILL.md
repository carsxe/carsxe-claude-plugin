---
name: plate-decoder
description: Look up vehicle information from a license plate number using the CarsXE API. Use this when a user mentions a license plate and wants to know what vehicle it belongs to.
---

When the user provides a license plate number (and optionally a US state or country):

1. Call the CarsXE Plate Decoder API:
   ```
   GET https://api.carsxe.com/v2/platedecoder?key={CARSXE_API_KEY}&plate={PLATE}&state={STATE}&country={COUNTRY}
   ```
2. Present the results: vehicle Make, Model, Year, VIN (if returned), and registration info.
3. If state or country are not provided, try with defaults (country=US) and note the response may be less precise.
4. If the API key is missing, tell the user to set the `CARSXE_API_KEY` environment variable.
