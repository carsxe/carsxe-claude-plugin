---
name: recalls-batch
description: Submit and retrieve bulk safety-recall checks for many VINs using the CarsXE Recalls Batch API. Use this when the user wants to check recalls for a fleet, inventory list, CSV of VINs, or more than a handful of vehicles at once.
---

When the user wants bulk recall checks (many VINs, a fleet, a CSV, or a spreadsheet):

1. **Submit** — POST at least one of `vins`, `csv`, or `csvUrl` (max 10,000 unique VINs):
   ```
   POST https://api.carsxe.com/v1/recalls-batch/submit?key={CARSXE_API_KEY}&source=claude_plugin
   Content-Type: application/json
   {"vins":["..."],"csv":"...","csvUrl":"...","webhookUrl":"..."}
   ```
   Include only provided fields. Return `batchId` and current `status`.
2. **Status** — poll until `completed`, `partial`, or `failed` (every 30–60 seconds; full processing often takes 30–60 minutes unless all VINs are cached):
   ```
   GET https://api.carsxe.com/v1/recalls-batch/status?key={CARSXE_API_KEY}&batchId={BATCH_ID}&source=claude_plugin
   ```
3. **Results** (JSON) once complete:
   ```
   GET https://api.carsxe.com/v1/recalls-batch/results?key={CARSXE_API_KEY}&batchId={BATCH_ID}&source=claude_plugin
   ```
4. **Download** (CSV) if the user wants a file:
   ```
   GET https://api.carsxe.com/v1/recalls-batch/download?key={CARSXE_API_KEY}&batchId={BATCH_ID}&source=claude_plugin
   ```
5. For a single VIN use `/v1/recalls`. For year/make/model with no VIN use `/v1/recalls-ymm`.
6. If the API key is missing, tell the user to set the `CARSXE_API_KEY` environment variable.
