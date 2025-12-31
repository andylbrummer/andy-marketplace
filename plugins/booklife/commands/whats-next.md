---
name: whats-next
description: Get personalized recommendation for what to read next based on your TBR, reading profile, and library availability
---

Help the user decide what to read next:

1. Get reading profile using profile_get to understand preferences
2. Get TBR list using tbr_list
3. For TBR books, check library availability
4. Analyze recent reading patterns (genres, completion rate, cadence)
5. Consider:
   - Books available immediately at library
   - Books matching recent genre preferences
   - High-priority TBR items
   - Series continuations
   - Mood-appropriate selections

Present top 3-5 recommendations with:
- Title and author
- Why it's suggested (matches your taste in X, available now, next in series, etc.)
- How to access it (library hold, already owned, etc.)
- Actionable next step with proper IDs

Make the recommendation feel personalized, not algorithmic. Explain the reasoning in a friendly way.

If TBR is empty or enrichment hasn't run:
- Suggest running enrichment for better recommendations
- Offer to search for books in favorite genres
- Ask about current reading mood or interests
