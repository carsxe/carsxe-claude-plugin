---
description: Connect or verify the hosted CarsXE MCP server via OAuth.
---

# CarsXE — Connect MCP

Confirm the hosted CarsXE MCP server is connected. Sign-in uses your CarsXE account (OAuth). Call the hosted MCP tools; do not make REST requests to `api.carsxe.com`.

## Steps

1. Check whether the `carsxe` MCP tools are available in this session (for example `get_vehicle_specs`, `decode_license_plate`, `get_market_value`).

2. If they are available, confirm:

   > CarsXE MCP is connected. You can use `/carsxe:*` commands and natural-language vehicle lookups. Usage is billed to your CarsXE plan.

3. If they are not available, walk the user through connecting. Do not invent extra config files or headers.

   **claude.ai / Cowork**
   - Open the plugin's Connectors tab
   - Add or connect the `carsxe` server at `https://mcp.carsxe.com/mcp`
   - Sign in with the CarsXE account when prompted, then retry the lookup

   **Claude Code**
   - After `/plugin install carsxe`, connect when prompted
   - Or open `/mcp`, enable the `carsxe` server bundled with this plugin, and complete the CarsXE sign-in
   - Then retry the lookup

4. Docs: https://docs.carsxe.com/docs/integrations/claude-quickstart

## Notes

- Authentication is the hosted MCP OAuth flow.
- If the session ends or the connector is disconnected, the user signs in again the same way.
- Usage is billed to the connected CarsXE plan.
