# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this
repository.

## Project Overview

Claude Code plugin marketplace repository (name: `rcdailey-plugins`) containing plugins shared
across multiple projects.

## Repository Structure

```txt
.claude-plugin/marketplace.json       # Marketplace definition
plugins/<name>/
  .claude-plugin/plugin.json          # Manifest (only "name" required)
  agents/                             # Auto-loaded .md files
  commands/                           # Auto-loaded .md files
  skills/                             # Auto-loaded SKILL.md in subdirs
  hooks/hooks.json                    # Optional
  .mcp.json                           # Optional
  .lsp.json                           # Optional
```

## Critical Rules

- **VERSION UPDATES MANDATORY**: Every distinct plugin change MUST include a version bump in
  `plugin.json` following semver (major: breaking changes, minor: new features, patch: fixes). No
  exceptions.
- `.claude-plugin/` contains ONLY `plugin.json` - all component dirs at plugin root
- Default dirs (`commands/`, `agents/`, `skills/`) auto-load; manifest paths are for ADDITIONAL
  custom locations that supplement defaults
- All paths relative, starting with `./`
- Use `${CLAUDE_PLUGIN_ROOT}` in hooks/MCP configs for absolute plugin path
- Tool permissions explicit - never wildcards like `mcp__octocode__*`
- NEVER specify default values in JSON - omit fields to use defaults (minimal config preferred)

## Plugin Manifest Schema (plugin.json)

Only `name` is required. All other fields optional:

- `name`: Unique identifier (kebab-case, no spaces) - REQUIRED
- `version`: Semantic version (e.g., "1.0.0")
- `description`: Brief explanation of plugin purpose
- `author`: Object with `name`, optional `email` and `url`
- `homepage`: Documentation URL
- `repository`: Source code URL
- `license`: License identifier (e.g., "MIT")
- `keywords`: Array of discovery tags
- `commands`: string|array - Additional command paths (supplements `commands/`)
- `agents`: string|array - Additional agent paths (supplements `agents/`)
- `skills`: string|array - Additional skill paths (supplements `skills/`)
- `hooks`: string|object - Hook config path or inline config
- `mcpServers`: string|object - MCP config path or inline config
- `lspServers`: string|object - LSP config path or inline config
- `outputStyles`: string|array - Output style paths

## Agent Frontmatter

```yaml
---
name: agent-name
description: >
  When Claude should invoke this agent (shown in agent picker)
tools: Tool1, Tool2, mcp__server__tool
model: sonnet|haiku|opus
---
```

### Model Selection

- `haiku` - Focused tasks: validation, pattern matching, file scanning, search operations
- `sonnet` - Complex reasoning: documentation synthesis, multi-step analysis, nuanced guidance
- `opus` - Most demanding tasks requiring deepest reasoning (rarely needed for agents)

## Command Frontmatter

```yaml
---
description: Short description for command picker
argument-hint: [optional] [args]
allowed-tools: Tool1, Tool2
---
```

Use `$ARGUMENTS` in body for user input.

## Installation

```bash
/plugin marketplace add ~/code/claude-plugins        # Local dev
/plugin marketplace add rcdailey/claude-plugins      # From GitHub
/plugin install recyclarr@rcdailey-plugins --scope user
```

## Reference Documentation

- [Plugin Reference](https://code.claude.com/docs/en/plugins-reference)
