---
description: Submit and retrieve bulk safety-recall checks for many VINs via the CarsXE MCP server.
---

# CarsXE — Recalls Batch

Submit and retrieve bulk safety-recall checks for up to 10,000 VINs using the CarsXE MCP batch tools.

## Steps

1. Parse $ARGUMENTS to extract the action as the first token:
   - `submit` — start a batch (`submit_recalls_batch`)
   - `status` — poll a batch (`get_recalls_batch_status`)
   - `results` — fetch completed JSON results (`get_recalls_batch_results`)
   - `download` — download completed results as CSV (`download_recalls_batch`)

   Examples:
   - `/carsxe:recalls-batch submit 1HGBH41JXMN109186 5YJSA1E26HF000001`
   - `/carsxe:recalls-batch status brb_mnablbn7_wvbaqv`
   - `/carsxe:recalls-batch results brb_mnablbn7_wvbaqv`
   - `/carsxe:recalls-batch download brb_mnablbn7_wvbaqv`

2. If no action is provided, ask: "Please provide an action: `submit`, `status`, `results`, or `download` (e.g., `/carsxe:recalls-batch submit 1HGBH41JXMN109186`)."

3. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.

4. **submit**
   - Parse remaining arguments as:
     - one or more 17-character VINs
     - optional `csv=<inline CSV>`
     - optional `csvUrl=<HTTPS URL>`
     - optional `webhookUrl=<HTTPS URL>`
   - Provide at least one of VINs, `csv`, or `csvUrl`. Combined unique VIN count must not exceed 10,000.
   - Call `submit_recalls_batch` with only the fields that were provided (`vins`, `csv`, `csvUrl`, `webhookUrl`).
   - Present `batchId`, `status`, `totalVins`, `processedVins`, `hitCount`, and timestamps.
   - If status is still `uploading` or `processing`, tell the user to poll with `/carsxe:recalls-batch status <batchId>` every 30–60 seconds (typical turnaround is 30–60 minutes unless all VINs are cached).

5. **status**
   - Parse `batchId` (required).
   - Call `get_recalls_batch_status` with `{ "batchId": "<BATCH_ID>" }`.
   - Present status (`uploading` | `processing` | `completed` | `partial` | `failed`), progress (`processedVins` / `totalVins`), `hitCount`, `hitRate`, and `errorMessage` if failed.
   - If `completed` or `partial`, offer `/carsxe:recalls-batch results <batchId>`.

6. **results**
   - Parse `batchId` (required).
   - Call `get_recalls_batch_results` with `{ "batchId": "<BATCH_ID>" }`.
   - Present job summary, then each VIN: `hasRecalls`, `recallCount`, and recall titles / campaign numbers / remedy status.
   - If the batch is still processing, tell the user to wait and re-check status.

7. **download**
   - Parse `batchId` (required).
   - Call `download_recalls_batch` with `{ "batchId": "<BATCH_ID>" }`.
   - Save or display the CSV. If still processing, tell the user to wait.

8. Handle errors gracefully (missing VINs, invalid VIN, batch not found, not connected).

## Notes

- For a single VIN use `/carsxe:recalls`. For year/make/model with no VIN use `/carsxe:recalls-ymm`.
- `csvUrl` must be an HTTPS URL of a CSV file. Max file size: 5 MB.
