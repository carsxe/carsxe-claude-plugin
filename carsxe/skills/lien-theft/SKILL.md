---
name: lien-theft
description: Check for active liens and theft records on a vehicle by VIN using the CarsXE API. Use this when a user asks whether a car has a lien, is stolen, or wants to verify ownership is clean before buying.
---

When the user asks about liens, theft status, or ownership encumbrances on a vehicle:

1. Make an HTTP GET request:
   ```
   GET https://api.carsxe.com/v1/lien-theft?key={CARSXE_API_KEY}&vin={VIN}
   ```
2. Present the lien status and theft records clearly.
3. Highlight any active liens or theft flags prominently — these are critical red flags for buyers.
4. If the API key is missing, tell the user to set the `CARSXE_API_KEY` environment variable.
