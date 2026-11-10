# Get LinkedIn profile posts

Automatically get LinkedIn profile posts on linkedin.com. Pull someone's latest LinkedIn posts and reposts, up to 100, with text, age and engagement counts.

- Site: linkedin.com
- Address: `reduck/linkedin.com/get_profile_posts`
- Updated: 2026-10-22 (v14)
- Author: Reduck AI (reduck)

## About

Give it the slug from a LinkedIn profile URL, jane-doe in linkedin.com/in/jane-doe, and a count, and you get that person's recent activity back in feed order, their own posts mixed with whatever they reposted. It suits a quick look before a first message, or keeping an eye on what two or three rival founders post each week. A recruiter about to message a staff engineer might pull 20 entries, drop the plain reposts and find a post from three weeks ago about a Postgres migration with 40 comments under it. That is the opening line. Reaction, comment and repost counts are plain numbers as strings, null when zero, so convert them before sorting. Ages come as LinkedIn's relative labels such as 3w, media-only posts arrive with text null and no image link, and a run stops at 100. You also only see what your own signed-in account is allowed to see.

## Run it

Ask an AI agent connected to Reduck over MCP (`https://mcp.reduck.ai/mcp`) to run `reduck/linkedin.com/get_profile_posts`, or run it from a terminal:

```bash
npx @reduck-ai/cli@latest run --script reduck/linkedin.com/get_profile_posts
```

## Input

- `publicId` (string, required): LinkedIn public profile ID — the slug in linkedin.com/in/<publicId>/ (e.g. 'rob-love').
- `count` (integer, optional): Max posts to collect by scrolling the activity feed. Default 10; the feed may return fewer if exhausted.

## Output

- `posts` (array, required)

## Example output

Shape only: placeholder values generated from the output schema, not a real run.

```json
{
  "posts": [
    {
      "urn": "…",
      "text": "…",
      "author": "…",
      "postUrl": "https://example.com/item/123",
      "reposts": "…",
      "comments": "…",
      "headline": "…",
      "postedAgo": "…",
      "reactions": "…",
      "quotedPost": {
        "urn": "…",
        "text": "…",
        "author": "…",
        "postUrl": "https://example.com/item/123",
        "headline": "…",
        "postedAgo": "…",
        "authorProfileUrl": "https://example.com/item/123"
      },
      "repostedBy": "…",
      "isQuoteReshare": true
    }
  ]
}
```

## FAQ

### What does "Get LinkedIn profile posts" do?

Get a LinkedIn profile's recent posts from its activity feed by public ID, scrolling to load up to count posts. Returns each post's text, urn/url, age, engagement counts, and repost info.

### How do I automatically get LinkedIn profile posts on linkedin.com?

Ask an AI agent connected to Reduck to run reduck/linkedin.com/get_profile_posts, or run it from a terminal with the Reduck CLI: npx @reduck-ai/cli@latest run --script reduck/linkedin.com/get_profile_posts

### Is there a linkedin.com API to get LinkedIn profile posts?

You do not need one. "Get LinkedIn profile posts" drives the real linkedin.com pages in a browser, so it works whether or not linkedin.com offers an API for this.

### What information do I need to provide?

Required: publicId. Optional: count.

### What does it return?

It returns posts.

### Do I need to be logged in to linkedin.com?

Yes. It acts as you on linkedin.com: on your own Chrome it reuses your session, and on a Reduck-hosted browser it loads the linkedin.com cookies saved by the Reduck extension.

### Does it change anything on linkedin.com, or only read data?

It only reads. It looks things up on linkedin.com and changes nothing there.

### How do I run it?

Ask an AI agent connected to Reduck to run reduck/linkedin.com/get_profile_posts, or run it from a terminal with the Reduck CLI: npx @reduck-ai/cli@latest run --script reduck/linkedin.com/get_profile_posts

### Who maintains it?

It is part of Reduck's official curated catalogue.

### Can I get posts older than the latest 100?

No. The script has no offset or start input, so each run returns the newest entries up to 100, and anything further back in the activity feed is out of reach. Anything above 100 in count is treated as 100. A profile with fewer posts just returns fewer, and one with none returns an empty posts array.

### How do I keep only the person's own posts and skip reposts?

Filter on repostedBy, which is null on their own entries and holds the reposter's name on a plain repost. A repost with added thoughts has isQuoteReshare set to true, their words in text and the original in quotedPost. On a plain repost, postedAgo is when it was reposted and the counts come from the original post.

### Does it work for company pages?

No. It only reads personal profiles, resolving the slug you give it as a linkedin.com/in/ public ID. A slug that does not match a member comes back as an error saying no profile has that public ID.

### What happens if I am signed out or LinkedIn throttles the account?

The run fails with an error rather than returning partial data. A sign-in wall asks you to log in on the browser the script runs on, and an HTTP 999 response means the account or IP is being throttled, so space calls out and retry later.

Source: https://reduck.ai/explore/scripts/reduck/linkedin.com/get_profile_posts
