# Send LinkedIn message

Automatically send LinkedIn message on linkedin.com. Send a message on LinkedIn (classic messaging, not Sales Navigator) — reply in an existing conversation by thread URL, start a conversation with a connection by name, or message by profile URL. Optionally attach a file (image or document) alongside the text. Returns whether it sent, who it went to, and confirmation the message/attachment landed. Limited to 1st-degree or open-profile connections; InMail (paid) is a separate flow not handled here.

- Site: linkedin.com
- Address: `reduck/linkedin.com/send_message`
- Updated: 2026-11-09 (v34)
- Author: Reduck AI (reduck)

## Run it

Ask an AI agent connected to Reduck over MCP (`https://mcp.reduck.ai/mcp`) to run `reduck/linkedin.com/send_message`, or run it from a terminal:

```bash
npx @reduck-ai/cli@latest run --script reduck/linkedin.com/send_message
```

## Input

- `dry_run` (boolean, optional): When true, everything runs — the recipient is resolved, the attachment is staged and confirmed in the composer, and the text is typed — then the run stops before the Send click. Nothing is delivered: sent comes back false and dry_run true. Use it to verify a recipient, a message and an attachment are accepted without messaging a real person.
- `message` (string, optional): The message text to send. Line breaks are kept: a newline starts a new line and an empty line leaves a blank line between paragraphs. Optional if an attachment or fileBase64 is given; required (non-empty) otherwise.
- `filename` (string, optional): Filename to attach it as, e.g. photo.png. Required when fileBase64 is set; not used by the attachment input, which is stored under its own name.
- `mimeType` (string, optional): MIME type of the attachment. Inferred from the filename extension when omitted. Applies to fileBase64 only.
- `recipient` (string, optional): Start/continue a conversation by the person's display name (e.g. "Jane Doe"). Every match the compose typeahead offers is checked against this name token-by-token (accent/case-insensitive) and the first one that matches is used, so a group conversation or another person ranked above your target does not block the send. A multi-word name must match the row's first and last names in order: middle names and credentials may differ ("Marie Dupont" matches "Marie Claire Dupont", "Jane Doe, PhD" matches "Jane Doe"), but "Luc Martin" does not match "Jean-Luc Martin" and "Marie Claire Dupont" does not match "Marie Dupont". A single-word name only passes on an exact full-name match: "Chris" resolving to "Chris Anderson" is refused rather than messaging the wrong person. A name that matches nobody messageable (a misspelling, someone who is not a 1st-degree connection, or your own name) is refused as such. Prefer profileUrl when you have it. Pass exactly one of threadUrl, profileUrl or recipient.
- `threadUrl` (string, optional): Reply in an existing conversation: its /messaging/thread/<id>/ URL (from list_inbox). LinkedIn thread ids can rotate over time, so fetch this fresh via list_inbox immediately before use rather than caching it long-term. Pass exactly one of threadUrl, profileUrl or recipient.
- `attachment` (string, optional): A file to attach (image or document), supplied as a file rather than base64. Preferred over fileBase64: it carries no payload size ceiling. The file is attached under the name 'attachment', since a file input's key is its stored filename.
- `fileBase64` (string, optional): File contents to attach, base64-encoded (no data: prefix). Fallback for callers that cannot bind a file; prefer the attachment input. Combine with message for accompanying text.
- `profileUrl` (string, optional): Start/continue a conversation by the person's LinkedIn profile URL (from list_inbox's participants[].profileUrl, search_people, or get_profile), e.g. https://www.linkedin.com/in/<id>. Preferred over recipient: resolves the exact person directly with no name-search ambiguity. Pass exactly one of threadUrl, profileUrl or recipient.

## Output

- `sent` (boolean, required): False on a dry run, where nothing was delivered.
- `dry_run` (boolean, optional): True when this run stopped before the Send click. The attachment was still staged and confirmed, and the text still typed.
- `message` (string | null, optional)
- `filename` (string | null, optional)
- `recipient` (string | null, optional): The conversation counterpart LinkedIn actually resolved. Confirm it's who you meant.
- `threadUrl` (string | null, optional): The conversation's /messaging/thread/<id>/ URL when the page landed on one; null in compose-overlay flows (never a compose URL).
- `attachmentVisible` (boolean | null, optional): True when the newly sent message renders an image or the filename, confirming the attachment landed rather than only that a message was sent. Null when no attachment was requested, and null on a dry run, where nothing was sent to inspect — the composer preview check is what proves staging there.

## FAQ

### What does "Send LinkedIn message" do?

Send a message on LinkedIn (classic messaging, not Sales Navigator) — reply in an existing conversation by thread URL, start a conversation with a connection by name, or message by profile URL. Optionally attach a file (image or document) alongside the text. Returns whether it sent, who it went to, and confirmation the message/attachment landed. Limited to 1st-degree or open-profile connections; InMail (paid) is a separate flow not handled here.

### How do I automatically send LinkedIn message on linkedin.com?

Ask an AI agent connected to Reduck to run reduck/linkedin.com/send_message, or run it from a terminal with the Reduck CLI: npx @reduck-ai/cli@latest run --script reduck/linkedin.com/send_message

### Is there a linkedin.com API to send LinkedIn message?

You do not need one. "Send LinkedIn message" drives the real linkedin.com pages in a browser, so it works whether or not linkedin.com offers an API for this.

### What information do I need to provide?

Optional: dry_run, message, filename, mimeType, recipient, threadUrl, attachment, fileBase64, profileUrl.

### What does it return?

It returns sent, dry_run, message, filename, recipient, threadUrl, attachmentVisible.

### Do I need to be logged in to linkedin.com?

Yes. It acts as you on linkedin.com: on your own Chrome it reuses your session, and on a Reduck-hosted browser it loads the linkedin.com cookies saved by the Reduck extension.

### Does it change anything on linkedin.com, or only read data?

It makes changes on linkedin.com, like sending, posting, booking or buying something.

### How do I run it?

Ask an AI agent connected to Reduck to run reduck/linkedin.com/send_message, or run it from a terminal with the Reduck CLI: npx @reduck-ai/cli@latest run --script reduck/linkedin.com/send_message

### Who maintains it?

It is part of Reduck's official curated catalogue.

Source: https://reduck.ai/explore/scripts/reduck/linkedin.com/send_message
