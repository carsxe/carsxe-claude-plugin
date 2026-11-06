---
name: recalls-ymm
description: Check safety recalls by year, make, and model (no VIN) using the CarsXE MCP server. Use this when the user asks about recalls for a model line, or has year/make/model but no VIN.
---

When the user asks about recalls or safety issues for a year/make/model and does **not** have a VIN:

1. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
2. Call `get_recalls_by_ymm` with `year`, `make`, and `model`.
3. Present recall details:
   - Total `recall_count` and `has_recalls`
   - For each recall: campaign number, component, summary, consequence, remedy, report date
   - Highlight `park_it`, `park_outside`, or over-the-air remedy flags
4. If no recalls exist, clearly confirm the model line has no safety recalls.
5. Emphasize this is a model-line result, not a specific vehicle. If they later provide a VIN, use `get_vehicle_recalls` instead.
6. If the connector is not signed in, tell the user to run `/carsxe:auth` and sign in with their CarsXE account.
