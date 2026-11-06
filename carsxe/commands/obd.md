---
description: Decode an OBD-II diagnostic trouble code via the CarsXE MCP server.
---

# CarsXE — OBD Code Decoder

Decode an OBD diagnostic trouble code (DTC) provided in $ARGUMENTS using `decode_obd_code`.

## Steps

1. Parse $ARGUMENTS to extract the OBD code (required).
   Example: `/carsxe:obd P0300`

2. If no code is provided, ask: "Please provide an OBD code to decode (e.g., `/carsxe:obd P0300`)."

3. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.

4. Call `decode_obd_code` with `{ "code": "<CODE>" }`.

5. Present the decoded information clearly:
   - Code (e.g., P0300)
   - Description of the fault
   - System affected (engine, transmission, etc.)
   - Possible causes
   - Suggested fixes or next steps (if returned)

6. Add helpful context — e.g., whether this is a serious code that requires immediate attention or a minor issue.

7. Handle errors gracefully (invalid code format, no data found, not connected).
