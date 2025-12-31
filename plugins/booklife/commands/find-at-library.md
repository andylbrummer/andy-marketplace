---
name: find-at-library
description: Search for a book at the library and place a hold if desired
---

Help the user find and potentially borrow a book from the library.

Usage: `/booklife:find-at-library [book title or author]`

Workflow:
1. If no argument provided, ask what book to search for
2. Search library using libby_search with the query
3. Show results with:
   - Title and author
   - Format (ebook, audiobook, or both)
   - Availability status (available now vs waitlist)
   - Wait time if on waitlist
   - media_id for placing holds
4. For each result:
   - If available: Offer to help place immediate checkout
   - If waitlist: Show position and estimated wait, offer to place hold
5. If user wants to place hold:
   - Ask for format preference if both available
   - Confirm auto_borrow preference
   - Use libby_place_hold with media_id and format
   - Confirm hold placement
6. Optionally offer to add to Hardcover TBR if not already there

Present results clearly:
```
Found "The Name of the Wind" by Patrick Rothfuss:

Ebook: Available now! (3 copies)
  → Ready to borrow immediately

Audiobook: Waitlist (12 people, ~14 days wait)
  → Can place hold with auto-checkout

media_id: 12345
```

Make it easy to take action with clear next steps.
