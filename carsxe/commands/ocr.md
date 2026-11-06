---
description: Extract a VIN from a photo URL via the CarsXE MCP server.
---

# CarsXE — VIN OCR (Extract VIN from Image)

Extract a VIN from an image using the CarsXE MCP tool `extract_vin_from_image`.

## Steps

1. Parse $ARGUMENTS to get the image URL (required).
   Example: `/carsxe:ocr https://example.com/vin-photo.jpg`

2. If no image URL is provided, ask: "Please provide a publicly accessible image URL containing a VIN (e.g., `/carsxe:ocr https://example.com/vin-photo.jpg`)."

3. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.

4. Call `extract_vin_from_image` with `{ "imageUrl": "<IMAGE_URL>" }`.

5. Present the result:
   - Extracted VIN
   - Confidence score (if available)
   - Offer to immediately run `/carsxe:specs {extracted_vin}` to decode the full vehicle specs

6. Handle errors gracefully:
   - Image not readable or too low quality → suggest the user try a clearer photo
   - No VIN detected → suggest retrying with a better angle or lighting
   - Not connected → follow `/carsxe:auth`
