# CarsXE — Vehicle Images

Retrieve images for a vehicle using the CarsXE Images API.

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

3. Make an HTTP GET request:

   ```
   GET https://api.carsxe.com/images?key=<CARSXE_API_KEY>&make=<MAKE>&model=<MODEL>[&year=<YEAR>][&trim=<TRIM>][&color=<COLOR>][&transparent=<TRANSPARENT>][&angle=<ANGLE>][&photoType=<PHOTOTYPE>][&size=<SIZE>][&license=<LICENSE>]
   ```

   Replace `<CARSXE_API_KEY>` with the value of the environment variable `CARSXE_API_KEY`. Only include optional parameters if the user specified them.

4. Present the results:
   - List all returned image URLs
   - Display each image inline if the environment supports it
   - Label each image with angle/type if available

5. Handle errors gracefully (no images found, invalid params, auth error).
