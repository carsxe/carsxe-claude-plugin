---
name: recalls-ymm
description: Check safety recalls by year, make, and model (no VIN) using the CarsXE Recalls by YMM API. Use this when the user asks about recalls for a model line, or has year/make/model but no VIN.
---

When the user asks about recalls or safety issues for a year/make/model and does **not** have a VIN:

1. Call the CarsXE Recalls by YMM API:
   ```
   GET https://api.carsxe.com/v1/recalls-ymm?key={CARSXE_API_KEY}&year={YEAR}&make={MAKE}&model={MODEL}&source=claude_plugin
   ```
2. Present recall details:
   - Total `recall_count` and `has_recalls`
   - For each recall: NHTSA campaign number, component, summary, consequence, remedy, report date
   - Highlight `park_it`, `park_outside`, or over-the-air remedy flags
3. If no recalls exist, clearly confirm the model line has no safety recalls.
4. Emphasize this is a model-line result, not a specific vehicle. If they later provide a VIN, use `/v1/recalls` instead.
5. If the API key is missing, tell the user to set the `CARSXE_API_KEY` environment variable.
