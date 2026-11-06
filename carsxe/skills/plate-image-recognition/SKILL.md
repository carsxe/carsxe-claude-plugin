---
name: plate-image-recognition
description: Extract a license plate number from an image URL using the CarsXE MCP server. Use this when a user shares a photo of a vehicle or license plate and wants to identify the plate number.
---

When the user shares an image containing a license plate and wants to extract the plate number:

1. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
2. Call `read_license_plate_from_image` with `{ "imageUrl": "<IMAGE_URL>" }`.
3. Display the extracted plate number and confidence score.
4. Offer to immediately decode the plate using `decode_license_plate`.
5. If the image is unclear, suggest the user retry with a better photo.
6. If the connector is not signed in, tell the user to run `/carsxe:auth` and sign in with their CarsXE account.
