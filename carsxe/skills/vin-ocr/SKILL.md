---
name: vin-ocr
description: Extract a VIN from a photo or image URL using the CarsXE MCP server. Use this when a user shares an image of a vehicle or VIN plate and wants to identify the VIN.
---

When the user shares an image containing a VIN (photo of dashboard, door jamb, windshield, etc.):

1. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
2. Call `extract_vin_from_image` with `{ "imageUrl": "<IMAGE_URL>" }`.
3. Display the extracted VIN and confidence score.
4. Offer to immediately decode the VIN using `get_vehicle_specs`.
5. If the image quality is poor or the VIN can't be extracted, suggest the user try a clearer photo with better lighting and angle.
6. If the connector is not signed in, tell the user to run `/carsxe:auth` and sign in with their CarsXE account.
