---
name: vehicle-specs
description: Fetch full vehicle specifications from a VIN using the CarsXE MCP server. Use this when the user provides a VIN and wants to know details about a vehicle (make, model, year, engine, trim, equipment, etc.).
---

When the user provides a VIN and asks about vehicle specs, details, or information:

1. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
2. Call `get_vehicle_specs` with `{ "vin": "<VIN>" }`.
3. Present the results in a clean, organized format covering:
   - Basic info: Make, Model, Year, Trim
   - Engine: type, cylinders, displacement, horsepower, torque
   - Transmission & drivetrain
   - Fuel type and economy (city/highway/combined)
   - Body style, doors, seats
   - Standard & optional equipment
4. When the host supports MCP Apps UI, call `render_vehicle_card` with the structured result (always fetch specs first).
5. If the connector is not signed in, tell the user to run `/carsxe:auth` and sign in with their CarsXE account.
