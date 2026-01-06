---
description: Learn TRaSH Guides repository structure for researching custom formats, quality profiles, naming conventions, and quality definitions.
---

# TRaSH Guides Repository Structure

This skill provides structural knowledge for navigating the TRaSH-Guides/Guides repository locally.

## Repository Layout

The authoritative structure is defined in `metadata.json` at the repository root. Consult this file
first when uncertain about file locations.

### JSON Data Locations

Replace `{service}` with `radarr` or `sonarr`:

- `docs/json/{service}/cf/` - Individual custom format definitions (each file contains a single CF
  with its trash_id)
- `docs/json/{service}/cf-groups/` - Custom format groups (logical groupings of related CFs)
- `docs/json/{service}/quality-profiles/` - Quality profile configurations
- `docs/json/{service}/quality-size/` - Quality definitions and file size limits
- `docs/json/{service}/naming/` - Media naming format templates

### Markdown Documentation

For understanding usage context and recommendations:

- `docs/Radarr/radarr-setup-quality-profiles.md` - How quality profiles and custom formats work
  together in Radarr
- `docs/Radarr/Radarr-collection-of-custom-formats.md` - Complete CF descriptions and categories for
  Radarr
- `docs/Sonarr/sonarr-setup-quality-profiles.md` - Sonarr quality profile setup guide
- `docs/Sonarr/sonarr-collection-of-custom-formats.md` - Sonarr CF collection and descriptions

## Key Concepts

### Service Separation

Sonarr and Radarr have SEPARATE custom format definitions with different trash_ids, even for similar
concepts (audio, HDR, codecs). Always identify the correct service context before searching.

### Common Tasks

- **Finding a trash_id** - Search the `cf/` directory for the ID or CF name
- **Understanding a quality profile** - Read the `quality-profiles/` JSON and corresponding setup
  markdown
- **Checking naming formats** - Look in `naming/` directory for the service
- **Investigating CF groups** - Search `cf-groups/` for logical groupings
- **Troubleshooting missing CFs** - Verify the CF exists for the correct service (Radarr vs Sonarr
  confusion is common)

## Research Guidelines

- If data is not found, state this clearly
- If similar alternatives exist, mention them
- Never fabricate trash_ids or configurations
- Provide exact file paths when referencing content
- Distinguish between Sonarr and Radarr data explicitly
