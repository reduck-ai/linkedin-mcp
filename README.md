# Linkedin MCP

LinkedIn has no official MCP server, and its self-serve API cannot search people. This LinkedIn MCP server lets Claude, ChatGPT or Cursor search people and posts, read profiles, experience and your inbox, and message your connections, from your own signed-in LinkedIn.

- Product: Reduck MCP
- Updated: 2026-10-28

![One integration, every website](https://docs.reduck.ai/overview/one-integration-every-website.png)

[Reduck MCP](https://docs.reduck.ai) gives your agent reusable browser scripts for the sites that have no API. They run in your own Chrome, through the Reduck extension, where you are already signed in: no credentials exposed, and no bot detection.

**Get started:** [docs.reduck.ai](https://docs.reduck.ai)

## Overview

LinkedIn is where you check who someone is, what they work on and what they said last week. An AI agent can read your email and your CRM, but when you ask it about a person on LinkedIn, it searches the web and finds a stale snippet, or nothing at all.

## Why it's hard

LinkedIn gives an agent no way in. It publishes no MCP server, and its self-serve API stops at signing in and posting on your own profile: no people search, no other members' profiles, no inbox. So the LinkedIn MCP servers fall into two groups. The API-based ones (Composio, Zapier, the content tools) publish posts and read your own analytics. The ones that read profiles drive a logged-in LinkedIn session, either on your machine, with a Python or Docker install that only local clients can reach, or on the vendor's servers, with your session held there.

## How Reduck does it

Reduck is a hosted MCP server whose LinkedIn scripts run in your own Chrome, where you are already signed in to LinkedIn. Your agent sees what you see: people search with LinkedIn's filters, full profiles with experience and education, any member's recent posts, post search, your inbox, and messages to your connections. It sends nothing unless you ask. There is no developer app, no install on your machine and no second LinkedIn session somewhere else.

## Tools

| Script | What it does | Takes |
|---|---|---|
| `search_people` | People matching keywords and filters, 10 per page, with headline, location, degree and mutual connections | keywords, title, company, location id, page |
| `get_profile` | A profile's headline, about, location, followers, experience and education | a public id |
| `get_profile_experience` | Every position on a profile, one entry per role | a public id |
| `get_profile_posts` | A member's latest posts, with reactions, comments and reposts | a public id, how many |
| `search_posts` | Posts matching keywords, by relevance or newest first, with their authors and counts | keywords, how many |
| `get_post_reactors` | Who reacted to a post | its url |
| `list_inbox` | Your conversations, 20 per page, newest first or matching keywords, with the last message and the unread count | a folder and filter, or keywords; a cursor for the next page |
| `get_thread` | The messages of one conversation | its url |
| `send_message` | A message in a conversation or to a connection, with a dry run | a thread or profile url, the text |

Every script answers structured data: names, profile links, positions, dates, the text as LinkedIn shows it and its counts. The summary and the reasoning stay in your agent. The full list of LinkedIn scripts is in the [catalogue](https://reduck.ai/explore?host=linkedin.com).

## Connect it

1. Install the Reduck extension in Chrome and stay signed in to LinkedIn there.
2. Add Reduck to your client: [Claude Code](https://docs.reduck.ai/claude-code), [Claude Desktop](https://docs.reduck.ai/claude-desktop), [ChatGPT](https://docs.reduck.ai/chatgpt) or [any other MCP client](https://docs.reduck.ai/other-clients).
3. Ask: "Find 10 heads of growth at AI startups in Paris on LinkedIn and summarize what each one posted last."

## LinkedIn MCP servers compared

| | API-based MCPs (Composio, Zapier, content tools) | Local open-source servers | Hosted session services | Reduck |
|---|---|---|---|---|
| People search and other profiles | No | Yes | Yes | Yes |
| Your inbox | No | Yes | Yes | Yes |
| Setup | OAuth to a LinkedIn app | Python, uvx or Docker on your machine | Connect your LinkedIn on their site | Stay signed in to LinkedIn in Chrome |
| Works in ChatGPT | Yes | Only if you host it | Yes | Yes |
| Where your LinkedIn session runs | Not used | Your machine, in its own browser | Their servers | Your own Chrome |

Each of these servers by name, from stickerdaniel/linkedin-mcp-server to LinkMCP, Linked API, Unipile, Composio and Zapier, with what it can read and how you set it up: [the best LinkedIn MCP servers for Claude, compared](https://reduck.ai/use-cases/best-linkedin-mcp-servers).

## Who it's for

- Founders, sales and recruiters who research people on LinkedIn before a call
- Anyone who wants Claude or ChatGPT to read their LinkedIn inbox and draft the replies
- Developers who want LinkedIn in their agent without a LinkedIn developer app or a scraper account

## FAQ

### Is there an official LinkedIn MCP server?

No. LinkedIn publishes no MCP server and no Claude connector, so every LinkedIn MCP server is third-party. ChatGPT has an official LinkedIn plugin: its page says it looks up a professional's title, company, location and follower count and links to the full profile, and that availability depends on your plan and workspace. It does not list reading posts, full experience or your messages. Reduck is a third-party MCP server too: its LinkedIn scripts run in your own signed-in LinkedIn tab.

### Why not use the LinkedIn API?

LinkedIn's self-serve API lets an app sign you in and post on your own profile. Searching members, reading other people's profiles and reading your messages are not in it. That is why the API-based LinkedIn MCP servers mostly publish posts, and why the ones that read profiles drive a logged-in LinkedIn session instead.

### How is it different from stickerdaniel/linkedin-mcp-server on GitHub?

That project is open source and runs on your machine: it drives its own Chromium with your LinkedIn session, so you install it with uvx, Docker or a Claude Desktop bundle, and use it from a local client such as Claude Desktop, Claude Code or Cursor. ChatGPT only takes remote connectors, so it cannot reach a local server you do not host. Reduck is a hosted MCP server: you add one URL to Claude, ChatGPT or Cursor, and the scripts run in your own Chrome through the Reduck extension.

### How is it different from LinkMCP, Linked API or Unipile?

Those are hosted services that hold your LinkedIn session on their side: Linked API says it runs your account in a dedicated cloud browser, and LinkMCP says it does not use LinkedIn's official partner API. Reduck does not keep a LinkedIn session of its own: each script runs in the Chrome where you are already signed in, from your own connection, only when you or your agent asks.

### Can it send LinkedIn messages for me?

Yes, and only when asked. send_message replies in a conversation from your inbox or messages a 1st-degree connection or an open profile by profile URL; InMail is not handled. It has a dry run that types the message and stops before the Send click, so the agent can show you the exact text and the recipient first.

### Will LinkedIn restrict my account?

LinkedIn's User Agreement restricts automated access, and no tool can promise that LinkedIn will never act on an account. Reduck does not run a bot on its own: each script runs only when you or your agent asks, one at a time, in your own browser. Keep the volume and the pace of a person, read before you message, and leave mass outreach out of it.

### Does it work with ChatGPT, Claude and Cursor?

Yes. Reduck connects to ChatGPT, Claude, Claude Code, Codex, Cursor and any other MCP client. You ask in plain words, and the agent picks the LinkedIn scripts it needs.

Source: https://reduck.ai/use-cases/linkedin-mcp
