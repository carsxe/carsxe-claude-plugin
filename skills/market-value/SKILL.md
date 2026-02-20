---
name: market-value
description: Get the current market value of a vehicle from its VIN using the CarsXE API. Use this when a user asks how much a car is worth, wants to know its value, or is thinking about buying/selling a vehicle.
---

When the user asks about a vehicle's price, worth, or market value and has a VIN:

1. Call the CarsXE Market Value API:
   ```
   GET https://api.carsxe.com/v2/marketvalue?key={CARSXE_API_KEY}&vin={VIN}
   ```
2. Present the estimated market value clearly, including:
   - Current value estimate
   - Low / average / high range if available
   - Historical trend if available
3. Provide helpful context (e.g., whether the value is strong for its age/mileage if that info is available).
4. If the API key is missing, tell the user to set the `CARSXE_API_KEY` environment variable.
