# Get LinkedIn profile experience

Automatically get LinkedIn profile experience on linkedin.com. Get the full experience list from a LinkedIn profile's dedicated experience page by publicId, with grouped companies expanded to one entry per role. Returns positions (title, company, companyUrl, employmentType, dateRange, duration, location, description).

- Site: linkedin.com
- Address: `reduck/linkedin.com/get_profile_experience`
- Updated: 2026-10-22 (v14)
- Author: Reduck AI (reduck)

## Run it

Ask an AI agent connected to Reduck over MCP (`https://mcp.reduck.ai/mcp`) to run `reduck/linkedin.com/get_profile_experience`, or run it from a terminal:

```bash
npx @reduck-ai/cli@latest run --script reduck/linkedin.com/get_profile_experience
```

## Input

- `publicId` (string, required): LinkedIn public profile id — the part after /in/ in the profile URL
- `count` (integer, optional): Max top-level experience entries to load (a company grouping several roles counts as one entry). Omit to load all.

## Output

- `complete` (boolean, required): True when every experience entry was loaded. False when count stopped the list first.
- `positions` (array, required)

## FAQ

### What does "Get LinkedIn profile experience" do?

Get the full experience list from a LinkedIn profile's dedicated experience page by publicId, with grouped companies expanded to one entry per role. Returns positions (title, company, companyUrl, employmentType, dateRange, duration, location, description).

### How do I automatically get LinkedIn profile experience on linkedin.com?

Ask an AI agent connected to Reduck to run reduck/linkedin.com/get_profile_experience, or run it from a terminal with the Reduck CLI: npx @reduck-ai/cli@latest run --script reduck/linkedin.com/get_profile_experience

### Is there a linkedin.com API to get LinkedIn profile experience?

You do not need one. "Get LinkedIn profile experience" drives the real linkedin.com pages in a browser, so it works whether or not linkedin.com offers an API for this.

### What information do I need to provide?

Required: publicId. Optional: count.

### What does it return?

It returns complete, positions.

### Do I need to be logged in to linkedin.com?

Yes. It acts as you on linkedin.com: on your own Chrome it reuses your session, and on a Reduck-hosted browser it loads the linkedin.com cookies saved by the Reduck extension.

### Does it change anything on linkedin.com, or only read data?

It only reads. It looks things up on linkedin.com and changes nothing there.

### How do I run it?

Ask an AI agent connected to Reduck to run reduck/linkedin.com/get_profile_experience, or run it from a terminal with the Reduck CLI: npx @reduck-ai/cli@latest run --script reduck/linkedin.com/get_profile_experience

### Who maintains it?

It is part of Reduck's official curated catalogue.

Source: https://reduck.ai/explore/scripts/reduck/linkedin.com/get_profile_experience
