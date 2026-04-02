---
name: market-value
description: Get the current market value of a vehicle from its VIN using the CarsXE API. Use this when a user asks how much a car is worth, wants to know its value, or is thinking about buying/selling a vehicle.
---

When the user asks about a vehicle's price, worth, or market value and has a VIN:

1. Ask if they want to provide optional parameters to refine the estimate:
   - `state` — US state code (e.g., `CA`, `TX`) for regional pricing
   - `mileage` — current mileage to adjust the value
   - `condition` — vehicle condition: `excellent`, `clean`, `average`, or `rough`
2. Call the CarsXE Market Value API:
   ```
   GET https://api.carsxe.com/v2/marketvalue?key={CARSXE_API_KEY}&vin={VIN}&source=claude_plugin
   ```
   Append `&state=<STATE>`, `&mileage=<MILEAGE>`, and/or `&condition=<CONDITION>` if provided.
3. Present the estimated market value clearly, including:
   - Current value estimate
   - Low / average / high range if available
   - Historical trend if available
4. Provide helpful context (e.g., whether the value is strong for its age/mileage if that info is available).
5. If the API key is missing, tell the user to set the `CARSXE_API_KEY` environment variable.
