---
name: vehicle-images
description: Retrieve images of a vehicle by make, model, and year using the CarsXE MCP server. Use this when a user wants to see what a vehicle looks like or asks for photos of a specific car.
---

When the user asks to see images or photos of a vehicle (by make, model, year):

1. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
2. Call `get_vehicle_images` with `make` and `model`, plus `year` and other optional filters when known.
3. Display the returned image URLs, rendering them inline if the environment supports it.
4. Label images by type/angle if available.
5. If make/model are not available, ask the user for the missing info before calling the tool.
6. If the connector is not signed in, tell the user to run `/carsxe:auth` and sign in with their CarsXE account.
