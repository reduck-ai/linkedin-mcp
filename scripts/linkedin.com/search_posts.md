# Search LinkedIn posts

Automatically search LinkedIn posts on linkedin.com. Search LinkedIn posts by keyword, newest-first or by relevance. Returns each post's permalink (a lnkd.in short link) and activity urn, author name, profile URL and headline, full text, relative age, and reaction/comment/repost counts. Accepts limit (default 10) and sortBy ("relevance" | "date_posted").

- Site: linkedin.com
- Address: `reduck/linkedin.com/search_posts`
- Updated: 2026-10-30 (v20)
- Author: Reduck AI (reduck)

## Run it

Ask an AI agent connected to Reduck over MCP (`https://mcp.reduck.ai/mcp`) to run `reduck/linkedin.com/search_posts`, or run it from a terminal:

```bash
npx @reduck-ai/cli@latest run --script reduck/linkedin.com/search_posts
```

## Input

- `limit` (integer, optional): Maximum posts to return (default 10). Results are scrolled until this many cards have loaded; fewer come back when the query has fewer posts.
- `sortBy` (string, optional): Result ordering: relevance (default) or date_posted.
- `keyword` (string, optional): Search terms, as typed into LinkedIn's content search. "keywords" is accepted as an alias for this field (it is what LinkedIn's own URL calls it).
- `keywords` (string, optional): Alias for "keyword" — same meaning; pass either one.

## Output

- `posts` (array, required)
- `complete` (boolean, required): True only when LinkedIn showed the end of the results before limit was reached.
- `start` (number, optional)
- `total` (number | null, optional)

## FAQ

### What does "Search LinkedIn posts" do?

Search LinkedIn posts by keyword, newest-first or by relevance. Returns each post's permalink (a lnkd.in short link) and activity urn, author name, profile URL and headline, full text, relative age, and reaction/comment/repost counts. Accepts limit (default 10) and sortBy ("relevance" | "date_posted").

### How do I automatically search LinkedIn posts on linkedin.com?

Ask an AI agent connected to Reduck to run reduck/linkedin.com/search_posts, or run it from a terminal with the Reduck CLI: npx @reduck-ai/cli@latest run --script reduck/linkedin.com/search_posts

### Is there a linkedin.com API to search LinkedIn posts?

You do not need one. "Search LinkedIn posts" drives the real linkedin.com pages in a browser, so it works whether or not linkedin.com offers an API for this.

### What information do I need to provide?

Optional: limit, sortBy, keyword, keywords.

### What does it return?

It returns posts, start, total, complete.

### Do I need to be logged in to linkedin.com?

Yes. It acts as you on linkedin.com: on your own Chrome it reuses your session, and on a Reduck-hosted browser it loads the linkedin.com cookies saved by the Reduck extension.

### Does it change anything on linkedin.com, or only read data?

It only reads. It looks things up on linkedin.com and changes nothing there.

### How do I run it?

Ask an AI agent connected to Reduck to run reduck/linkedin.com/search_posts, or run it from a terminal with the Reduck CLI: npx @reduck-ai/cli@latest run --script reduck/linkedin.com/search_posts

### Who maintains it?

It is part of Reduck's official curated catalogue.

Source: https://reduck.ai/explore/scripts/reduck/linkedin.com/search_posts
