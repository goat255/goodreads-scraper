# AGENTS.md: Goodreads Scraper

Guide for AI agents (Claude, Codex, any MCP or HTTP client) that need book ratings and details.

## When to use it

Use this actor when a task needs ratings or details for books named by title or author: ranking a reading list, enriching a catalog, book market research or building a recommendations dataset.

## Call it

**MCP (recommended):** add the Apify MCP server with this actor enabled:

```json
{
  "mcpServers": {
    "apify": {
      "url": "https://mcp.apify.com/?actors=goat255/goodreads-scraper",
      "headers": { "Authorization": "Bearer YOUR_APIFY_TOKEN" }
    }
  }
}
```

**HTTP:** one synchronous call returns the rows:

```
POST https://api.apify.com/v2/acts/goat255~goodreads-scraper/run-sync-get-dataset-items?token=YOUR_APIFY_TOKEN
Content-Type: application/json

{"titles": ["an example novel"], "maxMatchesPerTitle": 1}
```

## Input

| Field | Type | Default | Meaning |
|---|---|---|---|
| `titles` | array of strings | required | Book titles or author names; one lookup per entry |
| `maxMatchesPerTitle` | integer | `5` | Matches per entry (1 to 5); `1` gives one clean row per title |
| `minRatingsCount` | integer | `0` | Skip books with fewer ratings than this |
| `proxyConfiguration` | object | residential | Leave the default on |

## Output: one row per book

| Field | Meaning |
|---|---|
| `bookId`, `workId` | Book and work ids |
| `title`, `fullTitle` | Title; title with series |
| `author`, `authorId`, `authorUrl` | Author |
| `averageRating`, `ratingsCount` | Rating and how many people rated it |
| `pages` | Page count |
| `description` | Plain text summary, or `null` |
| `coverImage`, `url` | Cover image and book link |

## Tips for agents

- Set `maxMatchesPerTitle` to `1` when you need a one-to-one join with your list.
- Rank by `ratingsCount` for popularity and by `averageRating` for quality; use both together.
- Raise `minRatingsCount` (for example `1000`) to keep only established books.

Store page: https://apify.com/goat255/goodreads-scraper
