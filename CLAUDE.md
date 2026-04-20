# CarsXE Plugin for Claude Code

## What This Is

Markdown-based Claude Code plugin. No build step. Files are command/skill definitions consumed directly by the Claude Code harness.

## Structure

```
.claude-plugin/marketplace.json   # Marketplace metadata
carsxe/
  .claude-plugin/plugin.json      # Plugin manifest
  commands/                       # 14 explicit slash commands (*.md)
  skills/                         # 11 auto-invoked skills (*/SKILL.md)
```

## Adding a Command

1. Create `carsxe/commands/<name>.md`
2. Follow existing command pattern: API URL, method, params, response format, error handling
3. Always include `key=$CARSXE_API_KEY&source=claude_plugin` in query params

## Adding a Skill

1. Create `carsxe/skills/<name>/SKILL.md`
2. Add YAML frontmatter with `name` and `description` (description drives auto-invocation trigger)
3. Follow existing skill pattern

## API

**Base URL:** `https://api.carsxe.com`

**Auth:** `CARSXE_API_KEY` env var — set via `/carsxe:auth <KEY>`, session-scoped, not persisted

**Required params on every request:** `key=<CARSXE_API_KEY>&source=claude_plugin`

| Command | Endpoint | Method |
|---------|----------|--------|
| auth | `/v1/auth/validate` | GET |
| specs | `/specs` | GET |
| plate | `/v2/platedecoder` | GET |
| value | `/v2/marketvalue` | GET |
| history | `/history` | GET |
| images | `/images` | GET |
| recalls | `/v1/recalls` | GET |
| intvin | `/v1/international-vin-decoder` | GET |
| ocr | `/v1/vinocr` | POST (JSON body) |
| lien | `/v1/lien-theft` | GET |
| plateocr | `/platerecognition` | POST (JSON body) |
| ymm | `/v1/ymm` | GET |
| obd | `/obdcodesdecoder` | GET |

## Versioning

Version lives in two places — keep in sync:
- `carsxe/.claude-plugin/plugin.json` → `version`
- `.claude-plugin/marketplace.json` → `version`

## Testing

No automated tests. Validate manually:
1. Install plugin locally via marketplace
2. Run `/carsxe:auth <KEY>` to authenticate
3. Test affected commands with real API calls
