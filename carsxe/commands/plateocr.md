# CarsXE — Plate Image Recognition

Extract a license plate number from an image using the CarsXE Plate Recognition API.

## Steps

1. Parse $ARGUMENTS to get the image URL (required).
   Example: `/carsxe:plateocr https://example.com/plate-photo.jpg`

2. If no image URL is provided, ask: "Please provide a publicly accessible image URL containing a license plate (e.g., `/carsxe:plateocr https://example.com/plate-photo.jpg`)."

3. Make an HTTP **POST** request:
   - **URL:** `https://api.carsxe.com/platerecognition?key=<CARSXE_API_KEY>`
   - **Headers:** `Content-Type: application/json`
   - **Body (JSON):**
     ```json
     {
       "image": "<IMAGE_URL>"
     }
     ```
     Replace `<CARSXE_API_KEY>` with the value of the environment variable `CARSXE_API_KEY`.

4. Present the result:
   - Extracted plate number
   - Country/region detected (if available)
   - Confidence score (if available)
   - Offer to immediately run `/carsxe:plate {extracted_plate} {country}` to decode the vehicle

5. Handle errors gracefully:
   - Image not readable → suggest a clearer photo with the plate visible and well-lit
   - No plate detected → suggest retrying with a straight-on angle
   - Auth error → remind the user to set the `CARSXE_API_KEY` environment variable
