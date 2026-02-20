# CarsXE — OBD Code Decoder

Decode an OBD diagnostic trouble code (DTC) provided in $ARGUMENTS using the CarsXE OBD Codes Decoder API.

## Steps

1. Parse $ARGUMENTS to extract the OBD code (required).
   Example: `/carsxe:obd P0300`

2. If no code is provided, ask: "Please provide an OBD code to decode (e.g., `/carsxe:obd P0300`)."

3. Make an HTTP GET request:

   ```
   GET https://api.carsxe.com/obdcodesdecoder?key=<CARSXE_API_KEY>&code=<CODE>
   ```

   Replace `<CARSXE_API_KEY>` with the value of the environment variable `CARSXE_API_KEY`.

4. Present the decoded information clearly:
   - Code (e.g., P0300)
   - Description of the fault
   - System affected (engine, transmission, etc.)
   - Possible causes
   - Suggested fixes or next steps (if returned)

5. Add helpful context — e.g., whether this is a serious code that requires immediate attention or a minor issue.

6. Handle errors gracefully (invalid code format, no data found, auth error).
