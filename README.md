[![Claude Code Plugin](https://img.shields.io/badge/Claude%20Code-Plugin-blue)](https://claude.com/plugins)

# CarsXE Plugin for Claude Code

Access the full suite of CarsXE vehicle data APIs directly from Claude Code — decode VINs, look up license plates, get market values, check history, recalls, liens, OBD codes, and more.

## Features

| Command                                    | Description                               |
| ------------------------------------------ | ----------------------------------------- |
| `/carsxe:auth <API_KEY>`                   | Validate and set your CarsXE API key      |
| `/carsxe:specs <VIN>`                      | Decode a VIN — full vehicle specs         |
| `/carsxe:plate <PLATE> <COUNTRY> [STATE]`  | Look up vehicle from license plate        |
| `/carsxe:value <VIN> [STATE] [MILEAGE] [CONDITION]` | Get current market value         |
| `/carsxe:history <VIN>`                    | Full vehicle history report               |
| `/carsxe:images <MAKE> <MODEL> [YEAR]`     | Fetch vehicle photos                      |
| `/carsxe:recalls <VIN>`                    | Check for open safety recalls             |
| `/carsxe:intvin <VIN>`                     | Decode international (non-US) VINs        |
| `/carsxe:ocr <IMAGE_URL>`                  | Extract VIN from a photo (POST)           |
| `/carsxe:lien <VIN>`                       | Check for liens and theft records         |
| `/carsxe:plateocr <IMAGE_URL>`             | Extract license plate from a photo (POST) |
| `/carsxe:ymm <YEAR> <MAKE> <MODEL> [TRIM]` | Look up vehicle by Year/Make/Model        |
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

Sign up at [api.carsxe.com](https://api.carsxe.com) and grab your API key.

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
/carsxe:value WBAFR7C57CC811956
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

**Decode an OBD code:**

```
/carsxe:obd P0300
```

## Skills (Auto-invoked)

Skills are automatically triggered by Claude based on the conversation context. For example:

- _"What are the specs of VIN WBAFR7C57CC811956?"_ → triggers `vehicle-specs`
- _"Does this car have any recalls?"_ → triggers `vehicle-recalls`
- _"What does the check engine code P0300 mean?"_ → triggers `obd-decoder`

## API Documentation

Full CarsXE API docs: [api.carsxe.com/docs](https://api.carsxe.com/docs)
