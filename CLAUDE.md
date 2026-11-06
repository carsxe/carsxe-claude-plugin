# CarsXE Plugin for Claude Code

## What This Is

Markdown-based Claude Code plugin. No build step. Files are command/skill definitions consumed directly by the Claude Code harness. Lookups go through the hosted CarsXE MCP server, not direct REST calls.

## Structure

```
.claude-plugin/marketplace.json   # Marketplace metadata
carsxe/
  README.md                       # Directory listing copy (required)
  LICENSE                         # MIT, Copyright (c) 2026 CarsXE, Inc.
  .mcp.json                       # Hosted MCP connector
  .claude-plugin/plugin.json      # Plugin manifest
  commands/                       # Explicit slash commands (*.md)
  skills/                         # Auto-invoked skills (*/SKILL.md)
```

## Adding a Command

1. Create `carsxe/commands/<name>.md`
2. Follow the existing command pattern: parse `$ARGUMENTS`, call the matching `carsxe` MCP tool, present the result, handle errors
3. If the MCP tools are unavailable, point the user to `/carsxe:auth` (OAuth connect). Do not make REST requests to `api.carsxe.com`.

## Adding a Skill

1. Create `carsxe/skills/<name>/SKILL.md`
2. Add YAML frontmatter with `name` and `description` (description drives auto-invocation trigger)
3. Follow existing skill pattern: invoke the matching MCP tool

## MCP

**Server URL:** `https://mcp.carsxe.com/mcp` (declared in `carsxe/.mcp.json`)

**Auth:** OAuth with a CarsXE account when the user connects the plugin. Usage is billed to their CarsXE plan.

**Docs:** https://docs.carsxe.com/docs/integrations/claude-quickstart

| Command | MCP tool |
|---------|----------|
| auth | Connect/verify the `carsxe` MCP server (OAuth) |
| specs | `get_vehicle_specs` (then `render_vehicle_card` when the host supports it) |
| plate | `decode_license_plate` |
| value | `get_market_value` (then `render_market_value` when the host supports it) |
| history | `get_vehicle_history` |
| images | `get_vehicle_images` |
| recalls | `get_vehicle_recalls` (then `render_recalls` when the host supports it) |
| recalls-ymm | `get_recalls_by_ymm` |
| recalls-batch | `submit_recalls_batch` / `get_recalls_batch_status` / `get_recalls_batch_results` / `download_recalls_batch` |
| intvin | `decode_international_vin` |
| ocr | `extract_vin_from_image` |
| lien | `check_lien_and_theft` |
| plateocr | `read_license_plate_from_image` |
| ymm | `get_year_make_model` |
| ymm-options | `get_ymm_options` |
| ownership | `get_ownership_by_vin` / `get_ownership_by_person` / `get_ownership_by_address` / `get_ownership_by_zip` |
| obd | `decode_obd_code` |

## Versioning

Version lives in two places — keep in sync:
- `carsxe/.claude-plugin/plugin.json` → `version`
- `.claude-plugin/marketplace.json` → `version`

## Testing

No automated tests. Validate manually:
1. Install the plugin locally via marketplace
2. Connect the `carsxe` MCP server (OAuth) — `/carsxe:auth` walks through this
3. Test affected commands with real lookups
