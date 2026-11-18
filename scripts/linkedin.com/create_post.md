# LinkedIn — Create post

Automatically create post on linkedin.com. Publish a text post to your LinkedIn feed now, or schedule it for a later date and time. Without scheduleDate/scheduleTime it creates a real, public post under your account immediately — not a draft or preview — and returns the post's link. With scheduleDate (M/D/YYYY) and scheduleTime (a quarter-hour such as "9:45 AM") it queues the post in LinkedIn's Scheduled posts instead and returns when it will publish; an identical post already queued is reported, not duplicated. Plain text with optional @mentions and a single image (images cannot be scheduled); polls and articles need a different flow. dry_run stops before the final Post/Schedule click. Requires being logged into LinkedIn. To list or cancel scheduled posts, use get_scheduled_posts / remove_scheduled_post.

- Site: linkedin.com
- Address: `reduck/linkedin.com/create_post`
- Updated: 2026-11-01 (v60)
- Author: Reduck AI (reduck)

## Run it

Ask an AI agent connected to Reduck over MCP (`https://mcp.reduck.ai/mcp`) to run `reduck/linkedin.com/create_post`, or run it from a terminal:

```bash
npx @reduck-ai/cli@latest run --script reduck/linkedin.com/create_post
```

## Input

- `text` (string, required): The post body. Plain text; newlines preserved. Any bare URL in the text auto-unfurls into LinkedIn's own link-preview card. Posted publicly ("Anyone") under the logged-in member. Confirm the exact text with the user before running this: it creates a real, public, immediate post under their account.
- `dry_run` (boolean, optional): When true, everything runs (the composer opens, the body is typed, mentions are resolved and any image is attached and confirmed) and then the run stops before clicking Post. Nothing is published: posted comes back false, url and shareUrn null, and dry_run true. Use it to verify text, mentions and an image are accepted without creating a real public post.
- `mentions` (array, optional): Names of members or pages to @mention, added in order at the end of text. A name that matches several of LinkedIn's suggestions fails and lists them: add words from the headline or company to the name until one is left.
- `attachment` (string, optional): A single image to attach. Preferred over imageBase64: it carries the bytes outside the argument payload, so there is no payload ceiling. Pass this or imageBase64, not both. Cannot be combined with scheduleDate/scheduleTime.
- `imageBase64` (string, optional): A single image to attach, base64-encoded (no data: prefix). Prefer the attachment input, which has no payload ceiling. Cannot be combined with scheduleDate/scheduleTime. Requires imageFilename.
- `scheduleDate` (string, optional): Schedule the post instead of publishing it now: the date to publish, as M/D/YYYY (e.g. "8/14/2026"), from today to 90 days ahead. Requires scheduleTime.
- `scheduleTime` (string, optional): Time of day to publish when scheduling, as one of LinkedIn's quarter-hour options in the browser's time zone (e.g. "9:15 AM"). Requires scheduleDate.
- `imageFilename` (string, optional): Filename for the imageBase64 attachment, e.g. chart.png. Required when imageBase64 is set. Not used by the attachment input, which carries its own name.
- `imageMimeType` (string, optional): MIME type of the imageBase64 attachment; inferred from imageFilename when omitted.

## Output

- `url` (string | null, required): The post's permalink; pass it to get_post or delete_post. Null when shareUrn is null.
- `posted` (boolean, required): True once this run published a new post. False when scheduled (see scheduled), or when an identical post or schedule already existed and nothing new was created (see already_present / alreadyScheduled). Always false on a dry run.
- `shareUrn` (string | null, required): The post's urn, e.g. urn:li:activity:7522571491226374144. Null when scheduled, on a dry run, and on an already_present hit whose card does not show its urn yet.
- `scheduled` (boolean, required): True if this run scheduled a post (new or already queued) instead of publishing it now.
- `account_used` (object, required): The account the post was published or scheduled under, read from the session.
- `scheduledFor` (string | null, required): When scheduled is true, the scheduled-posts panel's own text for the entry, e.g. "Preview of the scheduled post that will be published on Mon August 17, 2026 at 1:00 PM, click to see detail view". Null otherwise.
- `already_present` (boolean, required): True when a post with this text is among the account's most recent posts: nothing new was posted, and shareUrn and url point at that post. Never true when scheduling.
- `alreadyScheduled` (boolean, required): True if a scheduled post with this text was already in the account's Scheduled posts queue: nothing new was scheduled, and scheduledFor describes that entry.
- `verified_on_page` (boolean, required): True if the script read the write back: for a post, its permalink renders the text; for a scheduled post, the Scheduled posts panel lists it; for an already_present or alreadyScheduled hit, always true. Always false on a dry run.
- `dry_run` (boolean, optional): True when this run stopped before clicking Post and published nothing. The body was still typed, the mentions still resolved and any image still attached and confirmed.
- `mediaAttached` (boolean | null, optional): True when an image was requested and its preview came back into the composer before publishing. Null when no image was requested.

## FAQ

### What does "LinkedIn — Create post" do?

Publish a text post to your LinkedIn feed now, or schedule it for a later date and time. Without scheduleDate/scheduleTime it creates a real, public post under your account immediately — not a draft or preview — and returns the post's link. With scheduleDate (M/D/YYYY) and scheduleTime (a quarter-hour such as "9:45 AM") it queues the post in LinkedIn's Scheduled posts instead and returns when it will publish; an identical post already queued is reported, not duplicated. Plain text with optional @mentions and a single image (images cannot be scheduled); polls and articles need a different flow. dry_run stops before the final Post/Schedule click. Requires being logged into LinkedIn. To list or cancel scheduled posts, use get_scheduled_posts / remove_scheduled_post.

### How do I automatically create post on linkedin.com?

Ask an AI agent connected to Reduck to run reduck/linkedin.com/create_post, or run it from a terminal with the Reduck CLI: npx @reduck-ai/cli@latest run --script reduck/linkedin.com/create_post

### Is there a linkedin.com API to create post?

You do not need one. "LinkedIn — Create post" drives the real linkedin.com pages in a browser, so it works whether or not linkedin.com offers an API for this.

### What information do I need to provide?

Required: text. Optional: dry_run, mentions, attachment, imageBase64, scheduleDate, scheduleTime, imageFilename, imageMimeType.

### What does it return?

It returns url, posted, dry_run, shareUrn, scheduled, account_used, scheduledFor, mediaAttached, already_present, alreadyScheduled, verified_on_page.

### Do I need to be logged in to linkedin.com?

Yes. It acts as you on linkedin.com: on your own Chrome it reuses your session, and on a Reduck-hosted browser it loads the linkedin.com cookies saved by the Reduck extension.

### Does it change anything on linkedin.com, or only read data?

It makes changes on linkedin.com, like sending, posting, booking or buying something.

### How do I run it?

Ask an AI agent connected to Reduck to run reduck/linkedin.com/create_post, or run it from a terminal with the Reduck CLI: npx @reduck-ai/cli@latest run --script reduck/linkedin.com/create_post

### Who maintains it?

It is part of Reduck's official curated catalogue.

Source: https://reduck.ai/explore/scripts/reduck/linkedin.com/create_post
