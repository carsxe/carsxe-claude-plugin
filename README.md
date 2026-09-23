[![Claude Code Plugin](https://img.shields.io/badge/Claude%20Code-Plugin-blue)](https://claude.com/plugins)

# CarsXE Plugin for Claude Code

Access the full suite of [CarsXE](https://carsxe.com) vehicle data APIs directly from Claude Code — decode VINs, look up license plates, get market values, check history, recalls (VIN, YMM, or batch), YMM options, ownership, liens, OBD codes, and more.

## Features

| Command                                    | Description                               |
| ------------------------------------------ | ----------------------------------------- |
| `/carsxe:auth <API_KEY>`                   | Validate and set your CarsXE API key      |
| `/carsxe:specs <VIN>`                      | Decode a VIN — full vehicle specs ([Vehicle Specifications](https://carsxe.com/vehicle-specifications)) |
| `/carsxe:plate <PLATE> <COUNTRY> [STATE]`  | Look up vehicle from license plate ([Vehicle Plate Decoder](https://carsxe.com/vehicle-plate-decoder)) |
| `/carsxe:value <VIN> [STATE] [MILEAGE] [CONDITION]` | Get current market value ([Vehicle Market Value](https://carsxe.com/vehicle-market-value)) |
| `/carsxe:history <VIN>`                    | Full vehicle history report ([Vehicle History](https://carsxe.com/vehicle-history)) |
| `/carsxe:images <MAKE> <MODEL> [YEAR]`     | Fetch vehicle photos ([Vehicle Images](https://carsxe.com/vehicle-images)) |
| `/carsxe:recalls <VIN>`                    | Check for open safety recalls ([Vehicle Recalls](https://carsxe.com/vehicle-recalls)) |
| `/carsxe:recalls-ymm <YEAR> <MAKE> <MODEL>` | Check recalls by year/make/model (no VIN) ([Vehicle Recalls](https://carsxe.com/vehicle-recalls)) |
| `/carsxe:recalls-batch <ACTION> ...`       | Bulk recalls: submit / status / results / download ([Vehicle Recalls](https://carsxe.com/vehicle-recalls)) |
| `/carsxe:intvin <VIN>`                     | Decode international (non-US) VINs ([International VIN Decoder](https://carsxe.com/international-vin-decoder)) |
| `/carsxe:ocr <IMAGE_URL>`                  | Extract VIN from a photo (POST)           |
| `/carsxe:lien <VIN>`                       | Check for liens and theft records         |
| `/carsxe:plateocr <IMAGE_URL>`             | Extract license plate from a photo (POST) ([Vehicle Plate Decoder](https://carsxe.com/vehicle-plate-decoder)) |
| `/carsxe:ymm <YEAR> <MAKE> <MODEL> [TRIM]` | Look up vehicle by Year/Make/Model        |
| `/carsxe:ymm-options [YEAR] [MAKE] [MODEL]` | List year/make/model/trim/variant options |
| `/carsxe:ownership <TYPE> ...`             | Owner & resident lookup (Enterprise)      |
| `/carsxe:obd <CODE>`                       | Decode an OBD diagnostic trouble code     |

All commands also have corresponding **skills** that Claude auto-invokes based on context — no need to type a command, just describe what you need naturally.

## Installation

**Step 1: Add the CarsXE marketplace**

```bash
/plugin marketplace add carsxe/carsxe-claude-plugin
```

**Step 2: Install the plugin**

```bash
/plugin install carsxe
```

## Setup

### 1. Get your CarsXE API key

Sign up at [carsxe.com](https://carsxe.com) and grab your API key.

### 2. Set your API key

Get your API key from [Here](https://api.carsxe.com/dashboard/developer).

Run the auth command — it validates your key against the CarsXE API and sets it for the current session automatically:

```
/carsxe:auth your_api_key_here
```

## Usage Examples

**Decode a VIN:**

```
/carsxe:specs WBAFR7C57CC811956
```

**Look up a California plate:**

```
/carsxe:plate 7XER187 US CA
```

**Check market value:**

```
/carsxe:value WBAFR7C57CC811956 CA 45000 clean
```

Optional params: state (e.g. `CA`), mileage, condition (`excellent` | `clean` | `average` | `rough`)

**Get vehicle history:**

```
/carsxe:history WBAFR7C57CC811956
```

**Find vehicle images:**

```
/carsxe:images BMW X5 2019
```

**Check recalls:**

```
/carsxe:recalls WBAFR7C57CC811956
```

**Check recalls by year/make/model (no VIN):**

```
/carsxe:recalls-ymm 2023 Toyota Camry
```

**Bulk recall check:**

```
/carsxe:recalls-batch submit 1HGBH41JXMN109186 5YJSA1E26HF000001
/carsxe:recalls-batch status brb_mnablbn7_wvbaqv
/carsxe:recalls-batch results brb_mnablbn7_wvbaqv
```

**Decode an international VIN:**

```
/carsxe:intvin WF0MXXGBWM8R43240
```

**Extract VIN from a photo:**

```
/carsxe:ocr https://example.com/vin-photo.jpg
```

**Check liens and theft:**

```
/carsxe:lien WBAFR7C57CC811956
```

**Extract plate from a photo:**

```
/carsxe:plateocr https://example.com/plate-photo.jpg
```

**Look up by Year/Make/Model:**

```
/carsxe:ymm 2020 Toyota Camry LE
```

**List available years, makes, models, or variants:**

```
/carsxe:ymm-options
/carsxe:ymm-options 2023 Toyota
/carsxe:ymm-options dimension=variants year=2025 make=Lexus
```

**Look up registered owners (Enterprise):**

```
/carsxe:ownership vin 1FT8X3BT0BEA61538
/carsxe:ownership person John Sample "123 Example St" 90210
/carsxe:ownership address "123 Example St" 90210
/carsxe:ownership zip 90210 gender=F min_age=45
```

**Decode an OBD code:**

```
/carsxe:obd P0300
```

## Skills (Auto-invoked)

Skills are automatically triggered by Claude based on the conversation context. For example:

- _"What are the specs of VIN WBAFR7C57CC811956?"_ → triggers `vehicle-specs`
- _"Does this car have any recalls?"_ → triggers `vehicle-recalls`
- _"Any recalls on a 2023 Toyota Camry?"_ → triggers `recalls-ymm`
- _"Check recalls for this list of VINs"_ → triggers `recalls-batch`
- _"What Toyota models were sold in 2023?"_ → triggers `ymm-options`
- _"Who is the registered owner of this VIN?"_ → triggers `ownership`
- _"What does the check engine code P0300 mean?"_ → triggers `obd-decoder`

## API Documentation

Full CarsXE API docs: [docs.carsxe.com](https://docs.carsxe.com)

### Products

- [Vehicle History](https://carsxe.com/vehicle-history)
- [Vehicle Plate Decoder](https://carsxe.com/vehicle-plate-decoder)
- [Vehicle Specifications](https://carsxe.com/vehicle-specifications)
- [International VIN Decoder](https://carsxe.com/international-vin-decoder)
- [Vehicle Images](https://carsxe.com/vehicle-images)
- [Vehicle Recalls](https://carsxe.com/vehicle-recalls)
- [Vehicle Market Value](https://carsxe.com/vehicle-market-value)
