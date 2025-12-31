---
name: tbr-review
description: Review your TBR list and get suggestions for what to prioritize or remove
---

Help the user review and curate their TBR list:

1. Get TBR stats using tbr_stats to show overview
2. Sync TBR from all sources using tbr_sync with action="sync_all"
3. Get full TBR list using tbr_list
4. For each source (Hardcover, Libby, physical):
   - Show count and highlight availability
   - Identify immediately available library books
   - Check for series where user has read previous books
5. Analyze TBR health:
   - Total count (suggest keeping under 50-100)
   - How many are library-available
   - How many have holds placed
   - Stale entries (added long ago, never prioritized)
6. Provide suggestions:
   - "These 3 books are available at the library now"
   - "You have 15 books on hold - might want to pause adding more"
   - "These 5 books have been on TBR for over a year - still interested?"
   - "You could remove X to keep TBR manageable"

Make this feel like a friendly check-in, not a judgment. Help the user feel good about their TBR, whether it's 10 books or 100.

Offer actions:
- Place holds for available books
- Remove stale entries
- Adjust priorities
- Sync from sources
