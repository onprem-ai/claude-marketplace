# Manage Marketplace Plugins

You are a guide for users who want to add plugins to the onprem-ai marketplace.

## Overview

The onprem-ai marketplace is where users can discover and install plugins for their Claude Code setup. This guide will help you understand the plugin structure and add new plugins to the marketplace.

## Everything is a Plugin

In Claude Code, **everything is a plugin** - there's no distinction between "plugins" and "skills". Both are plugins, just with different configurations:

- **Skills** - Plugins with `skills` configuration pointing to `./skills/` directory
- **MCP Servers** - Plugins with `.mcp.json` configuration
- **Agents** - Plugins with `agents/` directory
- **Hooks** - Plugins with `hooks/` directory

## Why This Structure?

The nested structure (`skills/your-skill-name/SKILL.md`) is **required**, not optional:

1. **Namespacing** - The skill name becomes `/plugin-name:your-skill-name` (e.g., `/my-plugin:hello`)
2. **Conflict Prevention** - Multiple plugins can have a skill named `hello` without clashing
3. **Multiple Skills** - Each skill needs its own directory for supporting files (scripts, reference docs)
4. **Discovery** - Claude scans `skills/*/SKILL.md` to find skills

The `SKILL.md` file MUST be inside a subdirectory - it CANNOT be directly in `skills/`. This is by design.

## Plugin Structure - CORRECT WAY

⚠️ **IMPORTANT**: Skills MUST follow this structure:

```
plugin-name/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   └── your-skill-name/    # ← Subdirectory REQUIRED
│       └── SKILL.md        # The file MUST be named SKILL.md (all caps)
└── .mcp.json               # For MCP servers (optional)
```

**Key points:**
1. Skills go in `skills/` directory at plugin root
2. Each skill has its own **subdirectory** (required for namespacing)
3. The skill file MUST be named `SKILL.md` (all caps)
4. In `plugin.json`, use `"skills": "./skills/"` (not `commands`)
5. The skill invocation name comes from the frontmatter `name:` field in SKILL.md

### WRONG Structure (causes validation errors):
```
plugin-name/
└── skills/
    └── SKILL.md            # ❌ File directly in skills/, not in subdirectory
```

### WRONG plugin.json (causes validation errors):
```json
{
  "commands": "skills/my-skill.md"  // ❌ Old format, should use skills
}
```

## Plugin Manifest (plugin.json)

The `plugin.json` file in `.claude-plugin/` directory:

```json
{
  "name": "your-plugin-name",
  "description": "Plugin description",
  "version": "1.0.0",
  "skills": "./skills/"     // Points to skills directory
}
```

For MCP servers, add `.mcp.json` at plugin root:
```json
{
  "mcp-server-name": {
    "type": "http",
    "url": "https://...",
    "headers": {"x-api-key": "${API_KEY}"}
  }
}
```

## Adding a Plugin to the Marketplace

1. Create a new directory in `plugins/` with your plugin name
2. Add the plugin structure:
   - `.claude-plugin/plugin.json` with proper metadata
   - `skills/your-skill-name/SKILL.md` with frontmatter and instructions
   - `.mcp.json` (if MCP server)
3. Update `.claude-plugin/marketplace.json` to include your plugin
4. Validate: `claude plugin validate /path/to/your-plugin`
5. Commit and push changes

## Example Plugin Structure

```
plugins/
└── your-plugin-name/
    ├── .claude-plugin/
    │   └── plugin.json     // Must have "skills": "./skills/"
    ├── skills/
    │   └── your-skill-name/
    │       └── SKILL.md    // Frontmatter with name and description
    └── .mcp.json           // Optional, for MCP servers
```

## Testing Your Plugin

Before adding to the marketplace, test locally:

```bash
# Validate the plugin
claude plugin validate /path/to/your-plugin

# Add marketplace locally
claude plugin marketplace add ./path/to/claude-marketplace

# Install the plugin
claude plugin install your-plugin-name@onprem-ai
```

## Updating the Marketplace

After pushing changes to the marketplace, users need to run `/plugin marketplace update onprem-ai` in Claude Code to refresh the cache and get the latest plugin versions. This is necessary because Claude Code caches marketplace data locally and may not immediately reflect changes pushed to the GitHub repository.

## Marketplaces

- **onprem-ai** - The main marketplace for on-prem plugins
