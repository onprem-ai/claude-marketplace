# claude-marketplace

A registry of Claude Code plugins maintained by [onprem-ai](https://github.com/onprem-ai).

## Quick Install

### 1. Add the Marketplace

```bash
# In Claude Code run:
/plugin marketplace add onprem-ai/claude-marketplace
```

**Note**: After adding the marketplace, run `/plugin marketplace update onprem-ai` to refresh the cache. This ensures you get the latest plugin versions from GitHub.

### 2. List Plugins

```bash
# List all available plugins in the marketplace
/plugin marketplace list

# Get JSON output for scripting
/plugin marketplace list --json
```

### 3. Install a Plugin

```bash
# Install a plugin
/plugin install websearch-exa@onprem-ai
```

### 4. Update Plugins

```bash
# Update all plugins from the marketplace
/plugin marketplace update

# Reinstall a plugin
/plugin install plugin-name@onprem-ai
```

## Troubleshooting

If you encounter validation errors like `commands: Invalid input` after installing a plugin:

1. Run `/plugin marketplace update onprem-ai` to refresh the marketplace cache
2. Uninstall and reinstall the plugin: `/plugin uninstall websearch-exa@onprem-ai` then `/plugin install websearch-exa@onprem-ai`

This can happen when Claude Code caches an older version of the plugin before fixes were pushed to the repository.
