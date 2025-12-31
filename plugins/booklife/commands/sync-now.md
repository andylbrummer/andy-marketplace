---
name: sync-now
description: Sync all reading activity - Libby loans to Hardcover, enrich metadata, cache Libby tags
---

Run a comprehensive sync of all reading data:

1. First check sync status using sync tool with action="status"
2. Show preview of what will be synced using action="preview"
3. Ask user to confirm the sync
4. Run comprehensive sync using sync tool with action="sync_all"
5. Show summary of what changed:
   - Books marked as read in Hardcover
   - New metadata enriched
   - Libby tags cached
6. Report any errors or unmatched books

This command coordinates:
- Syncing Libby history to local database
- Marking returned Libby books as "read" in Hardcover
- Enriching books with Open Library/Google Books metadata
- Caching full book information for Libby tagged items

Provide clear before/after summary and next steps.
