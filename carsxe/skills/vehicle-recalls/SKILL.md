---
name: vehicle-recalls
description: Check for open safety recalls on a vehicle using the CarsXE MCP server. Use this when a user asks whether a car has any recalls, safety issues, or wants to know if their vehicle needs a recall repair.
---

When the user asks about recalls or safety issues:

- If they have a VIN, call `get_vehicle_recalls` with `{ "vin": "<VIN>" }`.
- If they have year/make/model but no VIN, call `get_recalls_by_ymm` instead.
- If they have many VINs (fleet, inventory, CSV), use the recalls-batch tools (`submit_recalls_batch`, `get_recalls_batch_status`, `get_recalls_batch_results`, `download_recalls_batch`).

If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.

1. Present recall details:
   - Total number of open recalls
   - For each recall: campaign number, component, defect description, remedy status
2. If no recalls exist, clearly confirm the vehicle has no open recalls.
3. Emphasize any safety-critical recalls.
4. When the host supports MCP Apps UI and this was a VIN lookup, call `render_recalls` with the structured result (always fetch recalls first).
5. If the connector is not signed in, tell the user to run `/carsxe:auth` and sign in with their CarsXE account.
