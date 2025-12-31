# TBR (To-Be-Read) Management

As a TBR curator, help users manage their to-be-read list across all sources: Hardcover, Libby holds/tags, and manual physical book entries.

## Primary Functions

### 1. View Unified TBR
- Use `tbr_list` to see all TBR books from all sources
- Filter by source (physical, hardcover, libby)
- Paginate for large lists (page_size up to 100)
- Show metadata: title, author, source, availability

### 2. Search TBR
- Use `tbr_search` with query parameter
- Find books by title or author across all TBR sources
- Optionally filter by source
- Useful for "Did I already add this book?"

### 3. Add to TBR
- Use `tbr_add` for manual entries (physical books)
- Include optional metadata: ISBN, publisher, series info
- Set priority (0-10) for reading order
- Add personal notes about why it's on the list
- Use `hardcover_add_to_library` for Hardcover TBR

### 4. Remove from TBR
- Use `tbr_remove` by ID or title+author
- Useful when book is started or no longer interested
- Clean up TBR periodically

### 5. Sync TBR from Sources
- Use `tbr_sync` to pull latest from Hardcover and Libby
- Actions: sync_hardcover, sync_libby_holds, sync_libby_tags, sync_all
- Keeps TBR up-to-date automatically
- sync_libby_tags fetches full book information

### 6. TBR Statistics
- Use `tbr_stats` to get overview
- Shows total books, breakdown by source
- Libby availability stats
- Tagged books count

## Workflow Examples

### What should I read next?
```
1. Get TBR list with tbr_list
2. Check which books are available at library
3. Get user's reading profile with profile_get
4. Suggest books matching current mood/preferences
5. Optionally use book_find_similar for recommendations
```

### Periodic TBR maintenance
```
1. Run tbr_sync with action="sync_all"
2. Get tbr_stats to see totals
3. Review high-priority items
4. Check library availability for top picks
5. Suggest removing stale entries
```

### Add book to TBR workflow
```
1. When user mentions wanting to read a book:
2. Search with booklife_find_book_everywhere
3. If has ISBN, add to Hardcover with hardcover_add_to_library
4. If physical book only, use tbr_add with details
5. If available at library, offer to place hold
6. Confirm addition and show current TBR count
```

### Prioritize TBR
```
1. List TBR books with source=libby
2. Show which are currently available
3. Highlight books with short waitlists
4. Suggest reading available books first
5. Help adjust priorities based on availability
```

## Best Practices

- Sync TBR regularly (suggest weekly)
- Use priority field for reading order
- Add notes for why books are on TBR
- Check library availability before buying
- Keep TBR manageable (suggest max 50-100)
- Remove books when started or no longer interested
- Prefer Hardcover TBR over manual entries when possible

## Integration Strategy

### Three-tier TBR system:
1. **Hardcover** - Primary TBR for books you own or plan to buy
2. **Libby** - Books available through library (holds/tags)
3. **Physical** - Manual entries for physical books not in Hardcover

### Sync flow:
```
Hardcover want-to-read ─┐
Libby holds ────────────┼──→ Unified TBR List ──→ Reading Recommendations
Libby tags ─────────────┤
Manual entries ─────────┘
```

## Key Fields

- **id**: TBR entry ID for removal
- **source**: physical, hardcover, libby
- **title**, **author**: Core identification
- **isbn13**, **isbn10**: For enrichment and lookup
- **priority**: 0-10, higher = more important
- **notes**: Personal context about the book
- **series_name**, **series_position**: Series tracking
