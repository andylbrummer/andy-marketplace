# Andy's Marketplace - Setup Guide

## Quick Start

### 1. Add the marketplace to Claude Code

```bash
/plugin marketplace add ~/work/andy-marketplace
```

### 2. List available plugins

```bash
/plugin list andy-marketplace
```

### 3. Install a plugin

```bash
/plugin install booklife@andy-marketplace
```

## Current Plugins

### BookLife
Reading life management powered by BookLife MCP server.

**Features**:
- Track reading across Hardcover and Libby
- Manage TBR list across multiple sources
- Discover books with personalized recommendations
- Check library availability and place holds
- Sync reading activity automatically

**Commands**:
- `/booklife:reading-status` - Current reading snapshot
- `/booklife:sync-now` - Sync all reading data
- `/booklife:whats-next` - Get reading recommendation
- `/booklife:find-at-library` - Search and hold books
- `/booklife:tbr-review` - Review TBR list

**Skills** (auto-trigger):
- Reading sync & management
- Library search & availability
- TBR management
- Book discovery & recommendations

**Requirements**:
- BookLife MCP server installed and configured
- Environment variables: `HARDCOVER_API_KEY`, `LIBBY_CLONE_CODE`

## Adding New Plugins

See the main README.md for instructions on creating new plugins.

## Marketplace Structure

```
andy-marketplace/
├── .claude-plugin/
│   └── marketplace.json       # Marketplace configuration
├── plugins/                   # All plugins
│   └── booklife/
│       ├── .claude-plugin/
│       │   └── manifest.json
│       ├── skills/            # AI agent skills
│       ├── commands/          # Slash commands
│       └── README.md
├── README.md                  # Main documentation
└── SETUP.md                   # This file
```

## Testing Locally

Before publishing, test the plugin:

```bash
# Validate plugin structure
/plugin validate ~/work/andy-marketplace/plugins/booklife

# Try the commands
/booklife:reading-status
```

## Publishing to Git

To share across machines or with others:

```bash
cd ~/work/andy-marketplace
git init
git add .
git commit -m "Initial marketplace setup with BookLife plugin"
git remote add origin <your-repo-url>
git push -u origin main
```

Then install from Git:
```bash
/plugin marketplace add username/andy-marketplace
```

## Auto-Enable Plugins

To automatically enable plugins in specific projects, add to `.claude/settings.json`:

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
    "booklife@andy-marketplace": true
  }
}
```
