---
name: setup-mcp
description: Install BookLife MCP server - uses npx booklife-mcp@latest with slop-mcp and standard config support
---

# BookLife MCP Server Setup

This skill provides adaptive installation of the BookLife MCP server for reading life management across Hardcover and Libby.

## Overview

BookLife MCP can be registered in two ways:
1. **Via slop-mcp** - Centralized management with search, discovery, and orchestration
2. **Via Claude config** - Standard MCP configuration in Claude Code settings

The MCP server command resolution follows this priority:
1. **npx -y booklife-mcp@latest** - Primary method (npm package, no installation required)
2. **~/.local/bin/booklife-mcp** - Fallback if exists (local binary installation)
3. **uv run** - Legacy method for Python/uv development installation

## Prerequisites

BookLife MCP requires API credentials:
- **HARDCOVER_API_KEY** - Get from https://hardcover.app/settings/api
- **LIBBY_CLONE_CODE** - Get from Libby app (Settings -> Copy To Another Device)

## Installation Flow

### Step 1: Gather Required Credentials

Before installation, ensure you have:

1. **Hardcover API Key**:
   - Go to https://hardcover.app/settings/api
   - Generate a new API key if needed
   - Copy and save securely

2. **Libby Clone Code**:
   - Open Libby app on your phone
   - Go to Settings (gear icon)
   - Tap "Copy To Another Device"
   - Note the 8-digit code displayed

### Step 2: Verify npm Package Availability

The BookLife MCP server is available as an npm package that requires no installation:

```bash
# Verify npx can access the package
npx -y booklife-mcp@latest --help
```

**If successful**: The npm package is available and ready to use with command `npx` and args `["-y", "booklife-mcp@latest"]`

**Optional: Check for local installations**
The following are optional fallback methods if npm is unavailable:

```bash
# Check for local binary
if [ -x "$HOME/.local/bin/booklife-mcp" ]; then
  echo "FOUND: ~/.local/bin/booklife-mcp"
  "$HOME/.local/bin/booklife-mcp" --version
fi

# Check for Python/uv installation
BOOKLIFE_DIRS=(
  "$HOME/work/booklife-mcp"
  "$HOME/projects/booklife-mcp"
  "$HOME/booklife-mcp"
)

for dir in "${BOOKLIFE_DIRS[@]}"; do
  if [ -d "$dir" ] && [ -f "$dir/pyproject.toml" ]; then
    echo "FOUND: $dir (legacy Python installation)"
    break
  fi
done
```

**Recommended command for registration**:
- **Primary**: `npx` with `["-y", "booklife-mcp@latest"]` (recommended)
- **Fallback binary**: `~/.local/bin/booklife-mcp` with `[]` (if npm unavailable)
- **Legacy Python**: `uv` with `["run", "--directory", "<path>", "booklife-mcp"]` (development only)

### Step 3: Detect slop-mcp Availability

Check if slop-mcp is available:

```
Call: mcp__plugin_slop-mcp_slop-mcp__manage_mcps
Parameters: { "action": "list" }
```

**If successful** (returns list of MCPs): slop-mcp is available, proceed to Step 5A
**If tool not found or errors**: slop-mcp not available, proceed to Step 5B

### Step 4A: Install via slop-mcp

When slop-mcp is available, register BookLife for centralized management.

#### Check if Already Registered

Look for "booklife-mcp" in the manage_mcps list response. If already registered, report status and skip registration.

#### Ask User for Scope Preference

Present the user with scope options:

| Scope | Location | Use Case |
|-------|----------|----------|
| `user` | `~/.config/slop-mcp/config.kdl` | Personal setup, persists across projects |
| `project` | `.slop-mcp.kdl` | Team-shared, committed to repo |
| `memory` | Runtime only | Temporary, testing |

Default recommendation: `user` for persistent personal installation.

#### Ask for Credentials

Prompt user for their credentials:
- HARDCOVER_API_KEY
- LIBBY_CLONE_CODE

#### Register BookLife-MCP

**Primary method (npm package - recommended):**
```
Call: mcp__plugin_slop-mcp_slop-mcp__manage_mcps
Parameters: {
  "action": "register",
  "name": "booklife-mcp",
  "command": "npx",
  "args": ["-y", "booklife-mcp@latest"],
  "env": {
    "HARDCOVER_API_KEY": "<user's key>",
    "LIBBY_CLONE_CODE": "<user's code>"
  },
  "scope": "<user's choice>"
}
```

**Fallback method (local binary):**
```
Call: mcp__plugin_slop-mcp_slop-mcp__manage_mcps
Parameters: {
  "action": "register",
  "name": "booklife-mcp",
  "command": "/home/<user>/.local/bin/booklife-mcp",
  "args": [],
  "env": {
    "HARDCOVER_API_KEY": "<user's key>",
    "LIBBY_CLONE_CODE": "<user's code>"
  },
  "scope": "<user's choice>"
}
```

**Legacy method (Python/uv development installation):**
```
Call: mcp__plugin_slop-mcp_slop-mcp__manage_mcps
Parameters: {
  "action": "register",
  "name": "booklife-mcp",
  "command": "uv",
  "args": ["run", "--directory", "<BOOKLIFE_PATH>", "booklife-mcp"],
  "env": {
    "HARDCOVER_API_KEY": "<user's key>",
    "LIBBY_CLONE_CODE": "<user's code>"
  },
  "scope": "<user's choice>"
}
```

#### Verify Registration

```
Call: mcp__plugin_slop-mcp_slop-mcp__search_tools
Parameters: { "query": "hardcover", "mcp_name": "booklife-mcp" }
```

If tools are returned, registration was successful.

### Step 4B: Standard Installation (No slop-mcp)

When slop-mcp is not available, configure via Claude Code's MCP settings.

#### Create MCP Configuration

Create or update Claude Code's MCP configuration file:

**Location**: `~/.config/claude/claude_desktop_config.json`

**Primary method (npm package - recommended):**
```json
{
  "mcpServers": {
    "booklife-mcp": {
      "command": "npx",
      "args": ["-y", "booklife-mcp@latest"],
      "env": {
        "HARDCOVER_API_KEY": "your-hardcover-api-key",
        "LIBBY_CLONE_CODE": "your-8-digit-code"
      }
    }
  }
}
```

**Fallback method (local binary):**
```json
{
  "mcpServers": {
    "booklife-mcp": {
      "command": "/home/username/.local/bin/booklife-mcp",
      "args": [],
      "env": {
        "HARDCOVER_API_KEY": "your-hardcover-api-key",
        "LIBBY_CLONE_CODE": "your-8-digit-code"
      }
    }
  }
}
```

**Legacy method (Python/uv development installation):**
```json
{
  "mcpServers": {
    "booklife-mcp": {
      "command": "uv",
      "args": ["run", "--directory", "/path/to/booklife-mcp", "booklife-mcp"],
      "env": {
        "HARDCOVER_API_KEY": "your-hardcover-api-key",
        "LIBBY_CLONE_CODE": "your-8-digit-code"
      }
    }
  }
}
```

#### Restart Claude Code

After configuration, restart Claude Code to load the new MCP server.

## Available Tools After Setup

### Hardcover Tools
| Tool | Description |
|------|-------------|
| `hardcover_get_my_library` | Get your reading list |
| `hardcover_update_reading_status` | Update status/progress/rating |
| `hardcover_add_to_library` | Add books to your library |

### Libby Tools
| Tool | Description |
|------|-------------|
| `libby_search` | Search library catalog |
| `libby_get_loans` | View current checkouts |
| `libby_get_holds` | View active holds |
| `libby_place_hold` | Place library holds |
| `libby_sync_tag_metadata` | Cache tagged books |
| `libby_tag_metadata_list` | List cached tags |

### Unified Tools
| Tool | Description |
|------|-------------|
| `booklife_find_book_everywhere` | Search all sources |
| `booklife_best_way_to_read` | Find best access method |

### TBR Tools
| Tool | Description |
|------|-------------|
| `tbr_list` | View unified TBR |
| `tbr_search` | Search TBR |
| `tbr_add` | Add manual entries |
| `tbr_remove` | Remove entries |
| `tbr_sync` | Sync from sources |
| `tbr_stats` | TBR statistics |

### Sync & Discovery Tools
| Tool | Description |
|------|-------------|
| `sync` | Universal sync tool |
| `enrichment_enrich_history` | Add metadata |
| `book_find_similar` | Content-based recommendations |
| `profile_get` | Reading profile analysis |

## Quick Test

Test Hardcover connection:
```
Call: mcp__booklife-mcp__hardcover_get_my_library
Parameters: { "status": "currently_reading" }
```

Test Libby connection:
```
Call: mcp__booklife-mcp__libby_get_loans
Parameters: {}
```

## Troubleshooting

### Hardcover API Issues
- Verify API key is correct and not expired
- Check https://hardcover.app/settings/api
- Ensure key has read/write permissions

### Libby Clone Code Issues
- Clone codes expire - generate a fresh one if needed
- Code must be exactly 8 digits
- Ensure you're connected to the same library

### MCP Server Not Loading
1. Check Claude Code logs for errors
2. Verify npx is installed: `npx --version`
3. Test the package directly: `npx -y booklife-mcp@latest --help`
4. Ensure Node.js is installed and in PATH
5. Restart Claude Code completely

### Tools Not Available
1. Verify MCP server is registered: check slop-mcp list or Claude config
2. Check for typos in environment variable names
3. Ensure booklife-mcp can start: `npx -y booklife-mcp@latest --help`
4. Look for startup errors in terminal output

## Security Notes

- Store API keys securely (use environment variables)
- Never commit credentials to version control
- Libby clone codes are temporary - regenerate periodically
- Consider using a secrets manager for production use

## Summary Output

After setup, provide the user with:

1. **Installation method used**: slop-mcp or standard
2. **Scope** (if slop-mcp): user/project/memory
3. **Verification status**: Tools available and working
4. **Connected accounts**: Hardcover username, Libby libraries
5. **Available tools**: List of booklife-mcp tools now accessible
6. **Next steps**: Suggest running `/booklife:reading-status` or `/booklife:sync-now` commands
