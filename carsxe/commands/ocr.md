# CarsXE — VIN OCR (Extract VIN from Image)

Extract a VIN from an image using the CarsXE VIN OCR API.

## Steps

1. Parse $ARGUMENTS to get the image URL (required).
   Example: `/carsxe:ocr https://example.com/vin-photo.jpg`

2. If no image URL is provided, ask: "Please provide a publicly accessible image URL containing a VIN (e.g., `/carsxe:ocr https://example.com/vin-photo.jpg`)."

3. Make an HTTP **POST** request:
   - **URL:** `https://api.carsxe.com/v1/vinocr?key=<CARSXE_API_KEY>`
   - **Headers:** `Content-Type: application/json`
   - **Body (JSON):**
     ```json
     {
       "image": "<IMAGE_URL>"
     }
     ```
     Replace `<CARSXE_API_KEY>` with the value of the environment variable `CARSXE_API_KEY`.

4. Present the result:
   - Extracted VIN
   - Confidence score (if available)
   - Offer to immediately run `/carsxe:specs {extracted_vin}` to decode the full vehicle specs

5. Handle errors gracefully:
   - Image not readable or too low quality → suggest the user try a clearer photo
   - No VIN detected → suggest retrying with a better angle or lighting
   - Auth error → remind the user to set the `CARSXE_API_KEY` environment variable
