# Andy's Plugin Marketplace

Personal development plugins for various projects and interests.

## Overview

This marketplace contains custom Claude Code plugins for:
- **Library & Books**: Book management, reading tracking, library integrations
- **Generative Art**: Creative coding tools and utilities
- **Physics & Mathematics**: Scientific computing and visualization helpers
- **Fitness & Health**: Personal fitness tracking and goal management
- **Learning & Goals**: Knowledge management and progress tracking
- **Communication**: Nonviolent Communication (NVC) tools and practices
- **AI Development**: Machine learning and AI project utilities

## Installation

### Add the Marketplace

**Local development:**
```bash
/plugin marketplace add ~/work/andy-marketplace
```

**From Git repository** (after pushing to GitHub/GitLab):
```bash
/plugin marketplace add username/andy-marketplace
```

### Install Plugins

```bash
# List available plugins
/plugin list andy-marketplace

# Install a specific plugin
/plugin install plugin-name@andy-marketplace
```

## Available Plugins

Currently, this marketplace is being set up. Check back soon for available plugins!

## Creating New Plugins

To add a new plugin to this marketplace:

1. Create plugin directory:
   ```bash
   mkdir -p ~/work/andy-marketplace/plugins/my-plugin/.claude-plugin
   ```

2. Create `manifest.json`:
   ```json
   {
     "name": "my-plugin",
     "version": "1.0.0",
     "description": "Plugin description",
     "author": {
       "name": "Andy"
     }
   }
   ```

3. Add skills, hooks, or prompts to the plugin directory

4. Update marketplace.json to include the new plugin:
   ```json
   {
     "name": "my-plugin",
     "source": "./plugins/my-plugin",
     "description": "Plugin description",
     "version": "1.0.0",
     "author": {
       "name": "Andy"
     },
     "category": "development",
     "keywords": ["tag1", "tag2"]
   }
   ```

5. Validate the plugin:
   ```bash
   /plugin validate ~/work/andy-marketplace/plugins/my-plugin
   ```

## Auto-Enable for Projects

To automatically enable marketplace plugins in specific projects, add to `.claude/settings.json`:

```json
{
  "extraKnownMarketplaces": {
    "andy-marketplace": {
      "source": {
        "source": "path",
        "path": "~/work/andy-marketplace"
      }
    }
  },
  "enabledPlugins": {
    "plugin-name@andy-marketplace": true
  }
}
```

## Structure

```
andy-marketplace/
├── .claude-plugin/
│   └── marketplace.json      # Marketplace configuration
├── plugins/                  # Plugin directory
│   ├── plugin-one/
│   │   ├── .claude-plugin/
│   │   │   └── manifest.json
│   │   └── skills/
│   └── plugin-two/
│       └── ...
└── README.md                 # This file
```

## Contributing

This is a personal marketplace, but feel free to fork and adapt for your own use!

## License

Personal use - adapt as needed for your own projects.
