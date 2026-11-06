# CarsXE for Claude

CarsXE gives Claude vehicle data: decode a VIN or license plate, check safety recalls, estimate market value, get specs, history, lien/theft and images, explain OBD-II codes, and read a VIN or plate from a photo.

Slash commands (for example `/carsxe:specs`) and auto-invoked skills call the hosted CarsXE MCP tools after you connect. Claude can also render vehicle, market-value, and recall cards when the host supports them.

## Setup

Install the plugin and connect when prompted. The plugin uses the hosted CarsXE MCP server (https://mcp.carsxe.com/mcp) and you sign in with your CarsXE account. Usage is billed to your CarsXE plan. Docs: https://docs.carsxe.com/docs/integrations/claude-quickstart

If the connector is not signed in, run `/carsxe:auth` for connection steps, or open the plugin Connectors tab and connect `carsxe`.

## Data and network destinations

This plugin sends the vehicle identifiers or images you provide to CarsXE, Inc. at mcp.carsxe.com and api.carsxe.com to perform the lookup. See https://carsxe.com/privacy-policy. Support: abraham@carsxe.com

## License

MIT
