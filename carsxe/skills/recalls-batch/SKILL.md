---
name: recalls-batch
description: Submit and retrieve bulk safety-recall checks for many VINs using the CarsXE MCP server. Use this when the user wants to check recalls for a fleet, inventory list, CSV of VINs, or more than a handful of vehicles at once.
---

When the user wants bulk recall checks (many VINs, a fleet, a CSV, or a spreadsheet):

If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.

1. **Submit** — call `submit_recalls_batch` with at least one of `vins`, `csv`, or `csvUrl` (max 10,000 unique VINs). Include `webhookUrl` only if provided. Return `batchId` and current `status`.
2. **Status** — poll `get_recalls_batch_status` with `batchId` until `completed`, `partial`, or `failed` (every 30–60 seconds; full processing often takes 30–60 minutes unless all VINs are cached).
3. **Results** once complete: call `get_recalls_batch_results` with `batchId`.
4. **Download** if the user wants a file: call `download_recalls_batch` with `batchId`.
5. For a single VIN use `get_vehicle_recalls`. For year/make/model with no VIN use `get_recalls_by_ymm`.
6. If the connector is not signed in, tell the user to run `/carsxe:auth` and sign in with their CarsXE account.
