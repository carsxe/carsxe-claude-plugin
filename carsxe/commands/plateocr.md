---
description: Extract a license plate number from a photo URL via the CarsXE MCP server.
---

# CarsXE — Plate Image Recognition

Extract a license plate number from an image using `read_license_plate_from_image`.

## Steps

1. Parse $ARGUMENTS to get the image URL (required).
   Example: `/carsxe:plateocr https://example.com/plate-photo.jpg`

2. If no image URL is provided, ask: "Please provide a publicly accessible image URL containing a license plate (e.g., `/carsxe:plateocr https://example.com/plate-photo.jpg`)."

3. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.

4. Call `read_license_plate_from_image` with `{ "imageUrl": "<IMAGE_URL>" }`.

5. Present the result:
   - Extracted plate number
   - Country/region detected (if available)
   - Confidence score (if available)
   - Offer to immediately run `/carsxe:plate {extracted_plate} {country}` to decode the vehicle

6. Handle errors gracefully:
   - Image not readable → suggest a clearer photo with the plate visible and well-lit
   - No plate detected → suggest retrying with a straight-on angle
   - Not connected → follow `/carsxe:auth`
