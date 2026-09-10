# CarsXE — Recalls Batch

Submit and retrieve bulk safety-recall checks for up to 10,000 VINs using the CarsXE Recalls Batch API.

## Steps

1. Parse $ARGUMENTS to extract the action as the first token:
   - `submit` — start a batch
   - `status` — poll a batch
   - `results` — fetch completed JSON results
   - `download` — download completed results as CSV

   Examples:
   - `/carsxe:recalls-batch submit 1HGBH41JXMN109186 5YJSA1E26HF000001`
   - `/carsxe:recalls-batch status brb_mnablbn7_wvbaqv`
   - `/carsxe:recalls-batch results brb_mnablbn7_wvbaqv`
   - `/carsxe:recalls-batch download brb_mnablbn7_wvbaqv`

2. If no action is provided, ask: "Please provide an action: `submit`, `status`, `results`, or `download` (e.g., `/carsxe:recalls-batch submit 1HGBH41JXMN109186`)."

3. **submit**
   - Parse remaining arguments as:
     - one or more 17-character VINs
     - optional `csv=<inline CSV>`
     - optional `csvUrl=<HTTPS URL>`
     - optional `webhookUrl=<HTTPS URL>`
   - Provide at least one of VINs, `csv`, or `csvUrl`. Combined unique VIN count must not exceed 10,000.
   - Make an HTTP **POST** request:
     - **URL:** `https://api.carsxe.com/v1/recalls-batch/submit?key=<CARSXE_API_KEY>&source=claude_plugin`
     - **Headers:** `Content-Type: application/json`
     - **Body (JSON):** include only the fields that were provided:
       ```json
       {
         "vins": ["<VIN>", "..."],
         "csv": "<CSV>",
         "csvUrl": "<URL>",
         "webhookUrl": "<URL>"
       }
       ```
   - Present `batchId`, `status`, `totalVins`, `processedVins`, `hitCount`, and timestamps.
   - If status is still `uploading` or `processing`, tell the user to poll with `/carsxe:recalls-batch status <batchId>` every 30–60 seconds (typical turnaround is 30–60 minutes unless all VINs are cached).

4. **status**
   - Parse `batchId` (required).
   - Make an HTTP GET request:
     ```
     GET https://api.carsxe.com/v1/recalls-batch/status?key=<CARSXE_API_KEY>&batchId=<BATCH_ID>&source=claude_plugin
     ```
   - Present status (`uploading` | `processing` | `completed` | `partial` | `failed`), progress (`processedVins` / `totalVins`), `hitCount`, `hitRate`, and `errorMessage` if failed.
   - If `completed` or `partial`, offer `/carsxe:recalls-batch results <batchId>`.

5. **results**
   - Parse `batchId` (required).
   - Make an HTTP GET request:
     ```
     GET https://api.carsxe.com/v1/recalls-batch/results?key=<CARSXE_API_KEY>&batchId=<BATCH_ID>&source=claude_plugin
     ```
   - Present job summary, then each VIN: `hasRecalls`, `recallCount`, and recall titles / NHTSA numbers / remedy status.
   - If the batch is still processing (HTTP 409), tell the user to wait and re-check status.

6. **download**
   - Parse `batchId` (required).
   - Make an HTTP GET request (returns `text/csv`, not JSON):
     ```
     GET https://api.carsxe.com/v1/recalls-batch/download?key=<CARSXE_API_KEY>&batchId=<BATCH_ID>&source=claude_plugin
     ```
   - Save or display the CSV. If still processing (HTTP 409), tell the user to wait.

7. Replace `<CARSXE_API_KEY>` with the value of the environment variable `CARSXE_API_KEY`. Handle errors gracefully (missing VINs, invalid VIN, batch not found, auth error).

## Notes

- For a single VIN use `/carsxe:recalls`. For year/make/model with no VIN use `/carsxe:recalls-ymm`.
- `csvUrl` must be HTTPS and hosted on an allowed provider (Google Sheets, GCS, S3, Dropbox, Azure Blob, DigitalOcean Spaces, Box). Max file size: 5 MB.
