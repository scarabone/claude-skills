---
name: book-tracker
description: Automatically enrich book entries in Notion database with Amazon (Kindle prices, ratings), Goodreads (ratings), and Atlanta-Fulton Public Library (availability). Use when user asks to add, track, log, or record a book to their reading list or book database.
---

# Book Tracker Skill

## Purpose
Automatically enrich book entries with data from Amazon (Kindle pricing, ratings), Goodreads (community ratings), and Atlanta-Fulton Public Library System (availability) when adding books to the user's Notion Books database.

## When to Use This Skill
- User asks to "add a book" with title and/or author
- User mentions tracking, logging, or recording a book
- User references their reading list or book database
- User asks about a book and whether they should add it

## Core Workflow

### Step 1: Gather Book Information
If the user provides:
- **Title only**: Search for the most popular/recent edition
- **Title + Author**: Search for specific book by that author
- **ISBN**: Use ISBN for exact match
- **Partial info**: Ask clarifying questions if ambiguous

### Step 2: Search Three Sources

#### Amazon Search
Search for: `[Title] by [Author] Kindle`

**Extract:**
- Amazon product URL (Kindle edition preferred, physical as backup)
- Kindle price (e.g., "$9.99", "Kindle Unlimited", "Free")
- Amazon rating (out of 5 stars, e.g., 4.4)
- Publication year if not already known

**Notes:**
- Prioritize Kindle/ebook editions per user preference
- If Kindle not available, note physical price
- Look for "Look Inside" feature for ebook confirmation

#### Goodreads Search
Search for: `[Title] [Author] site:goodreads.com`

**Extract:**
- Goodreads book page URL
- Community rating (out of 5 stars, e.g., 4.23)
- Number of ratings (for context on reliability)

**Notes:**
- Goodreads ratings are often more critical than Amazon
- Useful for seeing similar reader recommendations

#### Atlanta-Fulton Public Library System (AFPLS)
Search for: `[Title] [Author] site:afpls.org` or `[Title] [Author] Atlanta Fulton Public Library`

**Extract:**
- AFPLS catalog URL
- Availability status:
  - **Available**: Book is available for checkout
  - **Checked Out**: All copies currently checked out
  - **Not Available**: Not in AFPLS collection
  - **Not Checked**: Unable to verify (set as default if search unclear)

**Notes:**
- AFPLS has physical books, ebooks (OverDrive/Libby), and audiobooks
- Check for "Available" status in search results
- Ebook availability through Libby is a great free option

### Step 3: Create Notion Entry

Use the Notion Books database: `22678cdb-45a3-4758-bc71-a100487944de`
Data Source ID: `b48a7ace-f3b6-4e20-b9a7-99c87fafc462`

**Required fields:**
- Title (from user or search)
- Author (from user or search)
- Status: Default to "Want to Read"

**Enriched fields to populate:**
- Amazon Link: Full product URL
- Amazon Rating: Number (e.g., 4.4)
- Goodreads Link: Full book page URL
- Goodreads Rating: Number (e.g., 4.23)
- AFPLS Link: Catalog URL
- AFPLS Available: Select appropriate status
- Kindle Price: Text with price
- Year Published: Extract from Amazon/Goodreads if found
- Format: Set "Kindle" if Kindle available, "Library" if AFPLS has it

**Optional fields (if user specifies):**
- Genre: Fiction, Non-Fiction, Mystery, Thriller, Sci-Fi, Fantasy, Historical, Biography, Memoir, Self-Help
- My Rating: Only if user has read it and rates it
- Notes: Any user comments

### Step 4: Confirm with User

After creating the entry, provide a summary:
```
✅ Added "[Book Title]" by [Author] to your reading list!

📚 Quick Info:
- Kindle: $X.XX (Amazon rating: 4.4⭐)
- Goodreads: 4.2⭐ (from X ratings)
- AFPLS: Available / Checked Out / Not Available
- [Link to Notion entry]

Recommendation: [Kindle if affordable / Library if free / etc.]
```

## Special Cases

### Multiple Editions
- Prioritize Kindle/ebook per user preference
- Note if physical copy significantly cheaper
- Mention if available at library

### Series Books
- Note series name and book number in Notes field
- Ask if user wants to add entire series

### Unavailable Books
- Still create entry with available information
- Note what's missing in Notes field
- Suggest alternative sources

### Pre-orders / Upcoming Releases
- Note release date in Notes
- Show pre-order price if available
- Set Status to "Want to Read"

## Cost Awareness

Always mention cost considerations:
- **Free**: Available at AFPLS library
- **Kindle Unlimited**: Note if included
- **Price comparison**: "Kindle $9.99 vs. Free at library"
- **Sales**: Note if book is on sale

## Rules

**Always:**
- Search all three sources (Amazon, Goodreads, AFPLS)
- Populate as many fields as possible
- Provide cost-aware recommendations
- Include direct Notion link in confirmation

**Never:**
- Assume book details without searching
- Skip any of the three sources
- Create entry without enrichment data
- Forget to check library availability
