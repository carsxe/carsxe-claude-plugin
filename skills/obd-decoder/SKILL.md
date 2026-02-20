---
name: obd-decoder
description: Decode an OBD-II diagnostic trouble code (DTC) using the CarsXE API. Use this when a user mentions a check engine light code, DTC, or OBD code like P0300, C1234, B0001, or U0100.
---

When the user mentions an OBD/DTC code and wants to know what it means:

1. Make an HTTP GET request:
   ```
   GET https://api.carsxe.com/obdcodesdecoder?key={CARSXE_API_KEY}&code={CODE}
   ```
2. Present the decoded fault clearly: code, description, system affected, possible causes, and suggested fixes.
3. Add context on severity — whether it requires immediate attention or can wait.
4. If the API key is missing, tell the user to set the `CARSXE_API_KEY` environment variable.
