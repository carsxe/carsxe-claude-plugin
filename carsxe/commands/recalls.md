---
description: Check open safety recalls for a VIN via the CarsXE MCP server.
---

# CarsXE — Vehicle Recalls

Check for active recalls on a vehicle using the VIN provided in $ARGUMENTS via `get_vehicle_recalls`.

## Steps

1. Parse $ARGUMENTS to extract the VIN (required).
2. If no VIN is provided, ask: "Please provide a VIN to check for recalls (e.g., `/carsxe:recalls WBAFR7C57CC811956`)."
3. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
4. Call `get_vehicle_recalls` with `{ "vin": "<VIN>" }`.
5. Present recall information clearly:
   - Number of open recalls
   - For each recall: campaign number, component affected, description of defect, remedy available, date
   - Whether each recall has been remedied
6. If no recalls are found, clearly confirm the vehicle has no open recalls.
7. When the host supports MCP Apps UI, call `render_recalls` with the structured result from `get_vehicle_recalls` (always fetch recalls first).
8. Handle errors gracefully.

## Notes

- For year/make/model with no VIN use `/carsxe:recalls-ymm` (`get_recalls_by_ymm`).
- For many VINs at once use `/carsxe:recalls-batch`.
