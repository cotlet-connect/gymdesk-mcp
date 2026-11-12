# Gymdesk MCP server for ChatGPT and Claude

Connect Gymdesk to ChatGPT, Claude and other AI agents through Cotlet. Work with attendance, leads, memberships and member messages in your own signed-in account. Cotlet is independent and not affiliated with Gymdesk. If Gymdesk offers an official API for your needs, we recommend it.

## What you can ask

> Show the attendance report for this week.

> Add a lead with the name, contact details and program interest I provide. Ask me before saving.

> Send the message I approve to the member I choose. Ask me before sending.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Claude

Add `https://cotlet.dev/mcp/v1` as a custom connector in Claude and sign in with Cotlet.dev. Follow the steps in your Cotlet console.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Gymdesk tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers": {"gymdesk": {"command": "python3", "args": ["/absolute/path/to/gymdesk-mcp/gymdesk_agent.py", "serve"], "env": {"COTLET_API_KEY": "your-key"}}}}
```

Or with Docker:

```bash
docker build -t gymdesk-mcp .
docker run -i --rm -e COTLET_API_KEY gymdesk-mcp
```

Tools: `gymdesk_guide`, `gymdesk_status`, `gymdesk_open`, `gymdesk_read`, `gymdesk_click`, `gymdesk_type`, `gymdesk_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. Run from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 gymdesk_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 gymdesk_agent.py status    # is Gymdesk ready in your Cotlet.dev account
python3 gymdesk_agent.py guide     # Gymdesk screens and sign-in link
python3 gymdesk_agent.py read      # open Gymdesk, read the page, close the browser
python3 gymdesk_agent.py tools     # list Cotlet.dev tools
python3 gymdesk_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Gymdesk users

**How do I connect Gymdesk to ChatGPT or Claude?**

Sign up at cotlet.dev, log in to Gymdesk once in its Cloud Browser and add Cotlet to ChatGPT or Claude, following the steps in your console. No API key is needed. ChatGPT and Claude then work in your Gymdesk account through Cotlet, in their phone apps too.

**Can ChatGPT check members in to a class in Gymdesk?**

ChatGPT records the check-in for the member and session you name, the same as staff do at the front desk.

**Can ChatGPT message members in Gymdesk?**

ChatGPT writes the email or text and sends it to the lead, member or selected members you choose after you approve it. Texting needs Gymdesk's usage-billed texting add-on.

**Does Gymdesk have an API?**

No publicly documented Gymdesk API was found on 11 Nov 2026: its /api and /developers pages returned 404 and the help center has no API article. Gymdesk documents outbound automation webhooks. Cotlet works through your own Gymdesk sign-in.

**Is Cotlet affiliated with Gymdesk?**

No. Cotlet is independent and not affiliated with Gymdesk.

## Find it on

- [Gymdesk on Cotlet](https://cotlet.dev/integrations/gymdesk-api-mcp-server)
- [All Cotlet packages](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/gymdesk-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=gymdesk

Request access: https://cotlet.dev/signup?app=gymdesk&utm_source=github&utm_medium=readme&utm_campaign=gymdesk
