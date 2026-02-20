# CarsXE — License Plate Decoder

Decode the license plate provided in $ARGUMENTS using the CarsXE Plate Decoder API.

## Steps

1. Parse $ARGUMENTS to extract:
   - `plate` (required): the license plate number
   - `country` (required): 2-letter country code (e.g., `US`, `GB`, `DE`)
   - `state` (optional): 2-letter US state code (e.g., `CA`) — improves accuracy for US plates
   - `district` (optional): district or region within the country

   Examples:
   - `/carsxe:plate 7XER187 US CA` → plate=7XER187, country=US, state=CA
   - `/carsxe:plate AB123CD GB` → plate=AB123CD, country=GB

2. If `plate` or `country` are missing, ask: "Please provide a plate number and country code (e.g., `/carsxe:plate 7XER187 US CA`)."

3. Make an HTTP GET request:
   ```
   GET https://api.carsxe.com/v2/platedecoder?key=<CARSXE_API_KEY>&plate=<PLATE>&country=<COUNTRY>[&state=<STATE>][&district=<DISTRICT>]
   ```
   Replace `<CARSXE_API_KEY>` with the value of the environment variable `CARSXE_API_KEY`.

4. Present the results clearly:
   - Vehicle Make, Model, Year
   - VIN (if returned)
   - Registration details (if available)
   - Engine & trim info

5. Handle errors gracefully (plate not found, invalid country, missing API key).