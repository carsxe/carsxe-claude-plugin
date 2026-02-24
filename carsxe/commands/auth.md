# CarsXE — Set & Validate API Key

Validate the API key provided in $ARGUMENTS using the CarsXE Auth API. If valid, set it as the `CARSXE_API_KEY` environment variable for the current session automatically — no manual `export` or `set` required.

## Steps

1. Parse $ARGUMENTS to extract:
   - `key` (required): the CarsXE API key string to validate

2. If no key is provided, ask: "Please provide your CarsXE API key (e.g., `/carsxe:auth YOUR_API_KEY`)."

3. Make an HTTP GET request to validate the key:

   ```
   GET https://api.carsxe.com/v1/auth/validate?key=<KEY>
   ```

4. Evaluate the response:
   - If the response indicates the key is valid (e.g., `"valid": true` or a success status), proceed to step 5.
   - If the response indicates the key is invalid or the request fails, tell the user: "The API key provided is invalid. Please check your key and try again." — do not set anything.

5. Set `CARSXE_API_KEY` in the current session by running the appropriate shell command via the terminal tool:
   - **Mac/Linux:** `export CARSXE_API_KEY=<KEY>`
   - **Windows (cmd):** `set CARSXE_API_KEY=<KEY>`
   - **Windows (PowerShell):** `$env:CARSXE_API_KEY="<KEY>"`

   Detect the current platform and run the correct command automatically.

6. Confirm success to the user:
   > "Your CarsXE API key has been validated and set for this session. You can now use all `/carsxe:*` commands."

## Notes

- The key is never stored to disk — it is only set in the current shell session.
- If the session ends, the key will need to be set again (or added to the shell profile by the user for persistence).
- This command replaces any previously set `CARSXE_API_KEY` in the current session.
