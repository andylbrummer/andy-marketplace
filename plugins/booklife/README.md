# BookLife Plugin

Claude Code plugin for managing your reading life powered by the BookLife MCP server.

## Overview

This plugin provides intelligent skills and convenient commands for:
- Tracking reading across Hardcover and Libby
- Managing your TBR (to-be-read) list
- Discovering books and getting personalized recommendations
- Checking library availability and placing holds
- Syncing reading activity across platforms

## Prerequisites

**Required**: BookLife MCP server must be installed and configured in Claude Code.

See the [BookLife MCP project](https://github.com/yourusername/booklife-mcp) for installation instructions.

The MCP server requires:
- `HARDCOVER_API_KEY` - Get from https://hardcover.app/settings/api
- `LIBBY_CLONE_CODE` - Get from Libby app (Settings → Copy To Another Device)

## Installation

### Add the marketplace (if not already added)
```bash
/plugin marketplace add ~/work/andy-marketplace
```

### Install the plugin
```bash
/plugin install booklife@andy-marketplace
```

### Enable the plugin
The plugin should auto-enable. If not:
```bash
/plugin enable booklife@andy-marketplace
```

## Skills

The plugin provides several intelligent skills that Claude will use automatically when appropriate:

### Reading Sync & Management
Helps sync reading activity across Libby and Hardcover, update book statuses, and maintain accurate reading lists.

**Triggers**: When discussing reading progress, syncing libraries, or updating book status

### Library Search & Availability
Assists with finding books at the library, checking availability, and managing holds through Libby.

**Triggers**: When searching for books, checking library availability, or placing holds

### TBR Management
Manages your unified to-be-read list across Hardcover, Libby holds/tags, and manual entries.

**Triggers**: When discussing reading lists, adding books to TBR, or organizing what to read next

### Book Discovery & Recommendations
Finds books through content-based recommendations, reading profile analysis, and comprehensive searches.

**Triggers**: When asking for book recommendations, "books like X", or what to read next

## Commands

Quick-action commands for common tasks:

### `/booklife:reading-status`
Show current reading snapshot:
- Currently reading books
- Library checkouts with due dates
- Active holds with queue positions
- Ready-to-borrow highlights

### `/booklife:sync-now`
Run comprehensive sync:
- Sync Libby loans to Hardcover
- Enrich metadata from Open Library/Google Books
- Cache Libby tagged books
- Preview changes before applying

### `/booklife:whats-next`
Get personalized reading recommendation based on:
- Your TBR list
- Reading profile and preferences
- Library availability
- Recent reading patterns

### `/booklife:find-at-library [query]`
Search library and place holds:
- Search Libby catalog
- Show availability (instant or waitlist)
- Place holds with auto-checkout
- Add to Hardcover TBR

### `/booklife:tbr-review`
Review and curate your TBR:
- Show TBR stats across all sources
- Identify library-available books
- Suggest priorities
- Clean up stale entries

## Usage Examples

### Check what you're reading
```
/booklife:reading-status
```

### Sync your reading activity
```
/booklife:sync-now
```

### Get a recommendation
```
/booklife:whats-next
```

### Find a specific book at the library
```
/booklife:find-at-library Project Hail Mary
```

### Review your reading list
```
/booklife:tbr-review
```

### Natural language (skills trigger automatically)
```
"What books are due soon at the library?"
"Add The Name of the Wind to my TBR"
"Show me books similar to Piranesi"
"Sync my Libby history to Hardcover"
```

## MCP Tools Used

This plugin leverages these BookLife MCP tools:

**Hardcover**:
- `hardcover_get_my_library` - Get reading list
- `hardcover_update_reading_status` - Update status/progress/rating
- `hardcover_add_to_library` - Add books to Hardcover

**Libby**:
- `libby_search` - Search library catalog
- `libby_get_loans` - Current checkouts
- `libby_get_holds` - Active holds
- `libby_place_hold` - Place library holds
- `libby_sync_tag_metadata` - Cache tagged books
- `libby_tag_metadata_list` - List cached tags

**Unified**:
- `booklife_find_book_everywhere` - Search all sources
- `booklife_best_way_to_read` - Find best access method

**TBR**:
- `tbr_list` - View unified TBR
- `tbr_search` - Search TBR
- `tbr_add` - Add manual entries
- `tbr_remove` - Remove entries
- `tbr_sync` - Sync from sources
- `tbr_stats` - TBR statistics

**Sync & Enrichment**:
- `sync` - Universal sync tool
- `enrichment_enrich_history` - Add metadata
- `enrichment_status` - Check progress

**Discovery**:
- `book_find_similar` - Content-based recommendations
- `profile_get` - Reading profile analysis

## Architecture

```
┌─────────────────────────────────────┐
│      Claude Code + Plugin           │
│  ┌────────────┐  ┌───────────────┐  │
│  │   Skills   │  │   Commands    │  │
│  └────────────┘  └───────────────┘  │
└─────────────┬───────────────────────┘
              │
              ▼
┌─────────────────────────────────────┐
│       BookLife MCP Server           │
│  ┌──────────┐ ┌──────────┐         │
│  │Hardcover │ │  Libby   │         │
│  │ GraphQL  │ │   API    │         │
│  └──────────┘ └──────────┘         │
│  ┌──────────┐ ┌──────────┐         │
│  │OpenLibrary│ │  Local   │         │
│  │   API    │ │  Cache   │         │
│  └──────────┘ └──────────┘         │
└─────────────────────────────────────┘
```

## Tips

- Run `/booklife:sync-now` weekly to keep everything in sync
- Use enrichment for better recommendations (automatic in sync)
- Enable auto-borrow on holds for instant access when available
- Check `/booklife:reading-status` regularly for due dates
- Use `/booklife:tbr-review` monthly to keep TBR manageable

## Troubleshooting

**Plugin not working?**
1. Verify BookLife MCP server is installed: Check `~/.config/claude/claude_desktop_config.json`
2. Ensure environment variables are set: `HARDCOVER_API_KEY` and `LIBBY_CLONE_CODE`
3. Restart Claude Code after MCP configuration changes
4. Check MCP server logs for errors

**Skills not triggering?**
- Skills trigger based on conversation context
- Use commands for explicit actions
- Ensure plugin is enabled: `/plugin list`

**Sync issues?**
- Check Libby clone code is valid (8 digits)
- Verify Hardcover API key has not expired
- Check network connectivity for API calls

## Contributing

This is a personal plugin in a personal marketplace. Feel free to fork and adapt for your own use!

## License

Personal use - adapt as needed for your own reading management.
