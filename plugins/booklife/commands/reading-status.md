---
name: reading-status
description: Show current reading status - what you're reading, library loans, and recent activity
---

Show a comprehensive snapshot of your current reading life:

1. Get currently reading books from Hardcover using hardcover_get_my_library with status="reading"
2. Get current Libby loans using libby_get_loans
3. Get active library holds using libby_get_holds
4. Highlight any holds that are ready to borrow
5. Show due dates for loans
6. Display reading progress for in-progress books

Present as a clean, organized dashboard:
- Currently Reading (from Hardcover) with progress
- Library Checkouts (from Libby) with due dates
- Library Holds (from Libby) with queue positions
- Ready to Borrow (highlight these prominently)

Include actionable suggestions:
- Books due soon that need attention
- Holds ready to check out
- Stale reading progress to update
