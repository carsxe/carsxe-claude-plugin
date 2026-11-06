---
name: obd-decoder
description: Decode an OBD-II diagnostic trouble code (DTC) using the CarsXE MCP server. Use this when a user mentions a check engine light code, DTC, or OBD code like P0300, C1234, B0001, or U0100.
---

When the user mentions an OBD/DTC code and wants to know what it means:

1. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
2. Call `decode_obd_code` with `{ "code": "<CODE>" }`.
3. Present the decoded fault clearly: code, description, system affected, possible causes, and suggested fixes.
4. Add context on severity — whether it requires immediate attention or can wait.
5. If the connector is not signed in, tell the user to run `/carsxe:auth` and sign in with their CarsXE account.
