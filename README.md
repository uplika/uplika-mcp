# uplika MCP server

Hosted MCP server that lets an AI agent publish to the social accounts you connect, and read replies and insights back.

| | |
|---|---|
| Server URL | `https://api.uplika.com/mcp` (Streamable HTTP) |
| Auth | OAuth 2.1 with dynamic client registration and PKCE. The client registers itself, so there is no API key to paste. |
| Official MCP Registry | `com.uplika/uplika` |
| Docs | https://uplika.com/en/docs |
| Setup per agent | https://uplika.com/en/integrations |

This repository holds setup notes for the hosted server. The server itself is a hosted service and its code is not published here.

## Channels

As of 2026-09-30: Threads, Instagram, YouTube, Facebook, Bluesky and Telegram publish today. Naver Blog works through the uplika Chrome extension in your own browser. TikTok is in platform review. Current status and each channel's limits: https://uplika.com/en/docs/platforms

## Connect your agent

Connect at least one social account in the dashboard first. If no channel is connected, the approval screen stops and asks you to connect one.

### Claude (claude.ai)

Customize → Connectors → Add custom connector, paste `https://api.uplika.com/mcp`, press Add, then approve in the browser. A new chat shows uplika in the tool list.

### Claude Code

```sh
claude mcp add --transport http --scope user uplika https://api.uplika.com/mcp
```

`--scope user` adds it for every project. Without it, Claude Code adds the server to the current folder only. Type `/mcp` to check that uplika is listed.

### Codex

```sh
codex mcp add uplika --url https://api.uplika.com/mcp
```

This reads the server's details and opens the browser for approval by itself. `codex mcp login` is only needed later if the approval was revoked. `codex mcp list` shows uplika with OAuth.

### ChatGPT

Until uplika is listed in ChatGPT's app directory, add it in developer mode: Settings → Security and login → Developer mode, then Plugins → Add plugin (+) → Create app → Create MCP App with the server URL above and OAuth. Sign in and approve. After that it works in the ChatGPT app too.

### Other MCP agents

Paste this into the agent:

```text
Set up uplika so I can post to social media from right here.

1. Add this HTTP MCP server at user (global) scope, so it works in every project and not just this folder: https://api.uplika.com/mcp
2. When the approval screen opens in my browser, walk me through clicking Allow to finish.
3. Then list my connected social accounts so we can confirm it worked.

Tell me when it's done.
```

## What the agent can do

Publish text, images, video and threads, schedule posts that the server sends on time, read and answer replies, hide comments, and read insights. Publishing is asynchronous; pass `wait: true` to hold the answer until the platform confirms. Full tool list: https://uplika.com/en/docs/tools

## Pricing

Free plan, no card. https://uplika.com/en#pricing

## Support

support@uplika.com
