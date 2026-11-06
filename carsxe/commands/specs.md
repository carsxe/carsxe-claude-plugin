---
description: Decode a VIN into full vehicle specifications via the CarsXE MCP server.
---

# CarsXE — Vehicle Specifications (VIN Decoder)

Decode the VIN provided in $ARGUMENTS using the CarsXE MCP tool `get_vehicle_specs`.

## Steps

1. Parse $ARGUMENTS to extract:
   - `vin` (required): 17-character alphanumeric string

2. If no VIN is provided, ask: "Please provide a VIN to decode (e.g., `/carsxe:specs WBAFR7C57CC811956`)."

3. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.

4. Call `get_vehicle_specs` with `{ "vin": "<VIN>" }`.

5. Present the response in a clean, readable format including:
   - Make, Model, Year, Trim
   - Engine details (type, cylinders, displacement, horsepower)
   - Transmission & drivetrain
   - Fuel type & economy
   - Body style & dimensions
   - Equipment & features (if available)

6. When the host supports MCP Apps UI, call `render_vehicle_card` with the structured result from `get_vehicle_specs` (always fetch specs first).

7. Handle errors gracefully (invalid VIN, not connected, no data).

## Notes

- A valid VIN is exactly 17 characters (letters and numbers, no I, O, or Q).
- For non-US VINs, `/carsxe:intvin` (`decode_international_vin`) is often a better first lookup.
