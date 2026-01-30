---
name: temporal-verification
description: >
  MANDATORY date verification before ANY web search or time-relative query. Triggers on: 
  web_search tool use, "recent," "latest," "current," "last week/month/year," "new," 
  "updated," any query where recency affects accuracy. CRITICAL FAILURE MODE: Searching 
  for 2024 content when it's 2026, using stale year assumptions from training data. 
  Call user_time_v0 FIRST, anchor to actual current date, then construct time-appropriate 
  queries. This is not optional—training data confidently hallucinates incorrect years.
---

# Temporal Verification

## Prime Directive

**Call `user_time_v0` before any web search. No exceptions.**

Training data creates false confidence about dates. System prompt dates don't always register. Verify the actual current date before every search.

## Workflow

1. **Check date**: Call `user_time_v0`
2. **Anchor**: Note current year, calculate relative years
3. **Construct query**: Use correct years in search terms
4. **Search**: Execute with proper temporal context

## Date Anchoring

After calling `user_time_v0`, establish:

| Reference | Calculation |
|-----------|-------------|
| Current year | From `user_time_v0` |
| Last year | Current - 1 |
| "Recent" | Past 12 months |
| Two years ago | Likely outdated |

**Example (January 2026):**
- "Recent" = 2025-2026
- "Last year" = 2025  
- 2024 = two years ago
- 2023 = ancient history for software

## Query Construction

**Wrong:**
- `Home Assistant changes 2024` (stale)
- `Claude new features` (no year = training bias)
- `latest news` (ambiguous timeframe)

**Right:**
- `Home Assistant 2025 2026 changes`
- `Claude features 2026`
- `news January 2026`

## Triggers

Any of these = call `user_time_v0` first:
- Web search tool invocation
- "Recent," "latest," "current," "new"
- "Last week/month/year"
- "What's happening with..."
- Any query where stale info = wrong answer

## No Exceptions

Even if the system prompt states the date, verify with `user_time_v0`. The tool call forces temporal grounding that passive date awareness does not.
