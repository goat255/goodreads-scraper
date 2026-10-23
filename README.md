# Goodreads Scraper

Find the books readers actually love. Turn a list of titles or authors into clean book data: average rating, number of ratings, page count, cover image and description, one row per book. No login, no API key.

[![Watch the demo on YouTube](https://img.youtube.com/vi/8cpukfpEfeQ/maxresdefault.jpg)](https://www.youtube.com/watch?v=8cpukfpEfeQ)

**[Run it on Apify →](https://apify.com/goat255/goodreads-scraper)**

## What you get

For each title you pass in, its closest matching books with:

- **Ratings that mean something**: `averageRating` next to `ratingsCount`, so a loved classic stands apart from a book with five reviews.
- **Book details**: `title`, `fullTitle` (with series), `author`, `pages`, `description` as plain text and `coverImage`.
- **Ids and links**: `bookId`, `workId`, `authorId`, `authorUrl` and `url` for clean joins.
- **A quality filter**: `minRatingsCount` drops obscure editions and reprints.

```json
{
  "bookId": "10000001",
  "title": "An Example Novel",
  "fullTitle": "An Example Novel (Example Series, #1)",
  "author": "Jane Doe",
  "averageRating": 4.29,
  "ratingsCount": 1687230,
  "pages": 658,
  "description": "A short plain text summary of the book.",
  "coverImage": "https://example.com/covers/an-example-novel.jpg",
  "url": "https://example.com/book/an-example-novel"
}
```

## What people use it for

- Top 10 lists: rank a reading list by how many readers rated each book.
- Catalog enrichment: add ratings, page counts and covers to a bookstore or library list.
- Book market research across genres and authors.
- Datasets for recommendations and reading apps.

## Run it

From the Apify Console, paste your titles and press Start. Or call it from code:

```bash
curl -X POST "https://api.apify.com/v2/acts/goat255~goodreads-scraper/run-sync-get-dataset-items?token=YOUR_APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"titles": ["an example novel", "Jane Doe"], "maxMatchesPerTitle": 3, "minRatingsCount": 1000}'
```

## Use it from an AI agent

Works with Claude, Codex and any agent that speaks MCP or HTTP. See [AGENTS.md](AGENTS.md) for the input, output and a ready-made MCP setup.

## Pricing

Pay per book returned. Current prices are on the [Apify Store page](https://apify.com/goat255/goodreads-scraper).

## More actors

This page is a showcase; the actor itself runs on Apify. **[Check our profile for more such actors →](https://apify.com/goat255)**
