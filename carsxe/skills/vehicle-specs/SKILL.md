---
name: vehicle-specs
description: Fetch full vehicle specifications from a VIN using the CarsXE API. Use this when the user provides a VIN and wants to know details about a vehicle (make, model, year, engine, trim, equipment, etc.).
---

When the user provides a VIN and asks about vehicle specs, details, or information:

1. Call the CarsXE Specifications API:
   ```
   GET https://api.carsxe.com/specs?key={CARSXE_API_KEY}&vin={VIN}
   ```
2. Present the results in a clean, organized format covering:
   - Basic info: Make, Model, Year, Trim
   - Engine: type, cylinders, displacement, horsepower, torque
   - Transmission & drivetrain
   - Fuel type and economy (city/highway/combined)
   - Body style, doors, seats
   - Standard & optional equipment
3. If the API key is missing, tell the user to set the `CARSXE_API_KEY` environment variable.
