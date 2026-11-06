---
description: Fetch vehicle photos by make, model, and optional year via the CarsXE MCP server.
---

# CarsXE — Vehicle Images

Retrieve images for a vehicle using the CarsXE MCP tool `get_vehicle_images`.

## Steps

1. Parse $ARGUMENTS to extract:
   - `make` (required): vehicle manufacturer (e.g., BMW, Ford, Toyota)
   - `model` (required): vehicle model (e.g., X5, Mustang, Camry)
   - `year` (optional): 4-digit year (e.g., 2019)
   - `trim` (optional): specific trim level (e.g., Sport, Limited)
   - `color` (optional): vehicle color (e.g., red, black)
   - `transparent` (optional): `true` to return transparent background images
   - `angle` (optional): `front`, `side`, or `back`
   - `photoType` (optional): `interior`, `exterior`, or `engine`
   - `size` (optional): `Small`, `Medium`, `Large`, `Wallpaper`, or `All`
   - `license` (optional): `Public`, `Share`, `ShareCommercially`, `Modify`, or `ModifyCommercially`

   Example: `/carsxe:images BMW X5 2019`

2. If `make` or `model` are missing, ask the user to provide them.

3. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.

4. Call `get_vehicle_images` with `make` and `model`, plus optional filters the user specified.

5. Present the results:
   - List all returned image URLs
   - Display each image inline if the environment supports it
   - Label each image with angle/type if available

6. Handle errors gracefully (no images found, invalid params, not connected).
