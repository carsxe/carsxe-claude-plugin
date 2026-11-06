---
name: year-make-model
description: Look up vehicle data by Year, Make, and Model using the CarsXE MCP server. Use this when a user doesn't have a VIN but knows the year, make, and model of a vehicle and wants specs, trims, or features.
---

When the user wants to browse available years, makes, models, or trims (dropdowns, "which years was X sold"), use `get_ymm_options` instead of this specs lookup.

When the user asks about a vehicle by year, make, and model (without a VIN):

1. If the `carsxe` MCP tools are unavailable, follow `/carsxe:auth` to connect. Call the hosted MCP tools rather than REST endpoints.
2. Call `get_year_make_model` with `year`, `make`, `model`, and `trim` only if the user specified one.
3. Present available trims, engine options, features, and specs.
4. If the user didn't specify a trim, list all available trims for that year/make/model.
5. If the connector is not signed in, tell the user to run `/carsxe:auth` and sign in with their CarsXE account.
