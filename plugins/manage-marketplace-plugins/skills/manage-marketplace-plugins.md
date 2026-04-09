# Add Plugin to Marketplace

You are a guide for users who want to add plugins to the onprem-ai marketplace.

## Overview

The onprem-ai marketplace is where users can discover and install plugins for their Claude Code setup. This guide will help you understand the plugin structure and add new plugins to the marketplace.

## Everything is a Plugin

In Claude Code, **everything is a plugin** - there's no distinction between "plugins" and "skills". Both are plugins, just with different configurations:

- **Skills** - Plugins with `commands: "skills/SKILL.md"` in plugin.json
- **MCP Servers** - Plugins with `.mcp.json` configuration
- **Agents** - Plugins with `agents/` directory
- **Hooks** - Plugins with `hooks/` directory

All plugins share the same structure:
```
plugin-name/
├── .claude-plugin/
│   └── plugin.json
└── [skills/|agents/|hooks/|commands/|bin/]
```

## Plugin Structure

Each plugin in the marketplace needs:

1. **`.claude-plugin/plugin.json`** - Plugin metadata and type (skill/MCP/agent/hooks)
2. **Component files** - SKILL.md, .mcp.json, etc. based on plugin type

## Adding a Plugin to the Marketplace

1. Create a new directory in `plugins/` with your plugin name
2. Add the plugin structure with `.claude-plugin/plugin.json` and components
3. Update `.claude-plugin/marketplace.json` to include your plugin
4. Commit and push changes

## Example Plugin Structure

```
plugins/
└── your-plugin-name/
    ├── .claude-plugin/
    │   └── plugin.json
    ├── skills/
    │   └── SKILL.md          # For skills
    └── .mcp.json             # For MCP servers (optional)
```

## Testing Your Plugin

Before adding to the marketplace, test locally:

```bash
claude plugin marketplace add ./path/to/claude-marketplace
claude plugin install your-plugin-name@onprem-ai
```

## Marketplaces

- **onprem-ai** - The main marketplace for on-prem plugins
