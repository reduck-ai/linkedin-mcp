# Search LinkedIn people

Automatically search LinkedIn people on linkedin.com. Search LinkedIn people by keywords with optional title, name, company, school, currentCompanyIds/pastCompanyIds (numeric ids from get_company_info), connectionDegrees, connectionOf, geoUrn, and a page number (10 people per page). Returns page, total, hasNextPage and people (name, url, publicId, memberUrn, degree, headline, location, snippet, followers, the mutual-connections line, and the members in common as data: up to two named mutuals with their profile, and mutualCount).

- Site: linkedin.com
- Address: `reduck/linkedin.com/search_people`
- Updated: 2026-11-06 (v35)
- Author: Reduck AI (reduck)

## Run it

Ask an AI agent connected to Reduck over MCP (`https://mcp.reduck.ai/mcp`) to run `reduck/linkedin.com/search_people`, or run it from a terminal:

```bash
npx @reduck-ai/cli@latest run --script reduck/linkedin.com/search_people
```

## Input

- `page` (integer, optional): Result page, 10 people per page. Default 1. The same page returns the same people, so pages can be fetched in parallel. LinkedIn caps browsing at ~100 pages; free-tier accounts also hit a monthly commercial-use search limit.
- `title` (string, optional): Current job title keyword (LinkedIn 'Title' filter, exact-phrase quoted).
- `geoUrn` (string | array, optional): Location filter: one or more LinkedIn geo ids, OR-combined. This script takes no place names. To filter by a place, call suggest_locations({query:'Paris'}) first and pass the geoUrn of the suggestion you want (e.g. '106383538' for Paris, Île-de-France, France).
- `school` (string, optional): School name keyword.
- `company` (string, optional): Company name keyword (free-text 'Company' filter — use currentCompanyIds for an exact company).
- `keywords` (string, optional): Free-text search query.
- `lastName` (string, optional): Last name filter.
- `firstName` (string, optional): First name filter.
- `connectionOf` (string, optional): A member URN — the memberUrn value returned by this script's results or by get_profile (bare ACoAA… tail or full urn:li:fsd_profile:…, both accepted). Restricts results to that member's connections as LinkedIn reveals them to you: for a member outside your 1st degree that is exactly the people you have in common — your possible introducers. Works alone (no other filter needed) and composes with every other facet.
- `pastCompanyIds` (array, optional): Numeric LinkedIn companyIds — past employer facet, OR-combined.
- `connectionDegrees` (array, optional): Connection-degree facet, OR-combined.
- `currentCompanyIds` (array, optional): Numeric LinkedIn companyIds (from get_company_info) — current employer facet, OR-combined.

## Output

- `page` (integer, required)
- `total` (integer | null, required): 0 when LinkedIn shows its empty state. Null otherwise: LinkedIn shows no result count on a results page.
- `people` (array, required): The people on this page, in LinkedIn's order. Empty only when LinkedIn shows its empty state, or when every card is an out-of-network member LinkedIn does not name.
- `hasNextPage` (boolean | null, required): Whether LinkedIn offers a next page. False on the last page and on the empty state. Null only when a full page shows no pager.
- `hiddenCount` (integer, required): Cards on this page for out-of-network members LinkedIn does not name. They are counted here and not returned in people.

## FAQ

### What does "Search LinkedIn people" do?

Search LinkedIn people by keywords with optional title, name, company, school, currentCompanyIds/pastCompanyIds (numeric ids from get_company_info), connectionDegrees, connectionOf, geoUrn, and a page number (10 people per page). Returns page, total, hasNextPage and people (name, url, publicId, memberUrn, degree, headline, location, snippet, followers, the mutual-connections line, and the members in common as data: up to two named mutuals with their profile, and mutualCount).

### How do I automatically search LinkedIn people on linkedin.com?

Ask an AI agent connected to Reduck to run reduck/linkedin.com/search_people, or run it from a terminal with the Reduck CLI: npx @reduck-ai/cli@latest run --script reduck/linkedin.com/search_people

### Is there a linkedin.com API to search LinkedIn people?

You do not need one. "Search LinkedIn people" drives the real linkedin.com pages in a browser, so it works whether or not linkedin.com offers an API for this.

### What information do I need to provide?

Optional: page, title, geoUrn, school, company, keywords, lastName, firstName, connectionOf, pastCompanyIds, connectionDegrees, currentCompanyIds.

### What does it return?

It returns page, total, people, hasNextPage, hiddenCount.

### Do I need to be logged in to linkedin.com?

Yes. It acts as you on linkedin.com: on your own Chrome it reuses your session, and on a Reduck-hosted browser it loads the linkedin.com cookies saved by the Reduck extension.

### Does it change anything on linkedin.com, or only read data?

It only reads. It looks things up on linkedin.com and changes nothing there.

### How do I run it?

Ask an AI agent connected to Reduck to run reduck/linkedin.com/search_people, or run it from a terminal with the Reduck CLI: npx @reduck-ai/cli@latest run --script reduck/linkedin.com/search_people

### Who maintains it?

It is part of Reduck's official curated catalogue.

Source: https://reduck.ai/explore/scripts/reduck/linkedin.com/search_people
