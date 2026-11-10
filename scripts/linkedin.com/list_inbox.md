# List LinkedIn message inbox

Automatically list LinkedIn message inbox on linkedin.com. List or search the conversations of the classic LinkedIn messaging inbox (not Sales Navigator), 20 per page. Either pick the folder (focused, other, archived, spam) and one of the inbox filters (unread, connections, inmail, starred, jobs), newest activity first, or pass keywords to search like the inbox search box: it matches participant names, message text and conversation titles in every folder, most relevant first. Returns per conversation its thread URL and id, the other participants (name, profile URL, connection degree), whether it is read and its unread count, its categories, the last activity time and the last message (text, subject, sender, whether you sent it, attachments). Pass nextCursor as cursor, with the same other args, to read the next page. A null nextCursor or an empty page means there is nothing more. Listing does not mark any conversation as read.

- Site: linkedin.com
- Address: `reduck/linkedin.com/list_inbox`
- Updated: 2026-11-09 (v11)
- Author: Reduck AI (reduck)

## Run it

Ask an AI agent connected to Reduck over MCP (`https://mcp.reduck.ai/mcp`) to run `reduck/linkedin.com/list_inbox`, or run it from a terminal:

```bash
npx @reduck-ai/cli@latest run --script reduck/linkedin.com/list_inbox
```

## Input

- `limit` (integer, optional): Not supported since 13 Oct 2026: the run fails with a message saying so. Each run returns one page of 20; pass nextCursor as cursor for the next.
- `cursor` (string, optional): nextCursor from the previous page, with the same other args, to read the next 20 conversations. Omit for the first page.
- `filter` (string, optional): One of the inbox's filter pills, applied inside the folder. Omit for no filter.
- `folder` (string, optional): The inbox folder, as the folder menu shows it. Omit for focused, the main inbox.
- `keywords` (string, optional): Search the whole inbox, like its search box: matches participant names, message text and conversation titles, in every folder, most relevant first. Cannot be combined with folder or filter.
- `sinceIso` (string, optional): Not supported since 13 Oct 2026: the run fails with a message saying so. Page with cursor and stop when lastActivityAt is older than your date.
- `unreadOnly` (boolean, optional): Not supported since 13 Oct 2026: the run fails with a message saying so. Use filter: "unread".

## Output

- `nextCursor` (string | null, required): Pass as cursor for the next page; null when this is the last page.
- `conversations` (array, required)
- `filter` (string | null, optional)
- `folder` (string | null, optional)
- `keywords` (string | null, optional)

## FAQ

### What does "List LinkedIn message inbox" do?

List or search the conversations of the classic LinkedIn messaging inbox (not Sales Navigator), 20 per page. Either pick the folder (focused, other, archived, spam) and one of the inbox filters (unread, connections, inmail, starred, jobs), newest activity first, or pass keywords to search like the inbox search box: it matches participant names, message text and conversation titles in every folder, most relevant first. Returns per conversation its thread URL and id, the other participants (name, profile URL, connection degree), whether it is read and its unread count, its categories, the last activity time and the last message (text, subject, sender, whether you sent it, attachments). Pass nextCursor as cursor, with the same other args, to read the next page. A null nextCursor or an empty page means there is nothing more. Listing does not mark any conversation as read.

### How do I automatically list LinkedIn message inbox on linkedin.com?

Ask an AI agent connected to Reduck to run reduck/linkedin.com/list_inbox, or run it from a terminal with the Reduck CLI: npx @reduck-ai/cli@latest run --script reduck/linkedin.com/list_inbox

### Is there a linkedin.com API to list LinkedIn message inbox?

You do not need one. "List LinkedIn message inbox" drives the real linkedin.com pages in a browser, so it works whether or not linkedin.com offers an API for this.

### What information do I need to provide?

Optional: limit, cursor, filter, folder, keywords, sinceIso, unreadOnly.

### What does it return?

It returns filter, folder, keywords, nextCursor, conversations.

### Do I need to be logged in to linkedin.com?

Yes. It acts as you on linkedin.com: on your own Chrome it reuses your session, and on a Reduck-hosted browser it loads the linkedin.com cookies saved by the Reduck extension.

### Does it change anything on linkedin.com, or only read data?

It only reads. It looks things up on linkedin.com and changes nothing there.

### How do I run it?

Ask an AI agent connected to Reduck to run reduck/linkedin.com/list_inbox, or run it from a terminal with the Reduck CLI: npx @reduck-ai/cli@latest run --script reduck/linkedin.com/list_inbox

### Who maintains it?

It is part of Reduck's official curated catalogue.

Source: https://reduck.ai/explore/scripts/reduck/linkedin.com/list_inbox
