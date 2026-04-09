# claude-marketplace

A registry of Claude Code plugins maintained by [onprem-ai](https://github.com/onprem-ai).

## Quick Install

### 1. Add the Marketplace

```bash
# In Claude Code run:
/plugin marketplace add onprem-ai/claude-marketplace
```

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

## License

MIT
