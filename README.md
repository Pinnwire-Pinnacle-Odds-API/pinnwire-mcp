# PinnWire

Cursor plugin that connects agents to [PinnWire](https://pinnwire.com) through PinnWire's official remote [Model Context Protocol](https://modelcontextprotocol.io/) server.

Get current Pinnacle sports betting odds (live and prematch), recent price drops, and no-vig fair prices: the sharp reference line for +EV screens, arbitrage checks, and betting models.

## Install

1. Open **Cursor Settings → Plugins**.
2. Search for **PinnWire**.
3. Click **Install**. No sign-in is needed.

Or add the server to `.cursor/mcp.json` yourself, using the config below.

## MCP

```json
{
  "mcpServers": {
    "pinnwire": {
      "type": "http",
      "url": "https://pinnwire.com/mcp"
    }
  }
}
```

No auth is required. Without a key, calls use PinnWire's shared public demo (10 requests/minute, 50/day across all demo users). For your own quota, get a free key (100 requests/day, no card) at [pinnwire.com](https://pinnwire.com) and change the URL to `https://pinnwire.com/mcp?key=YOUR_KEY`, or send it as `"headers": {"Authorization": "Bearer YOUR_KEY"}`.

## What agents can do

| Tool | Capabilities |
| --- | --- |
| `list_sports` | The 13 covered sports and their `sport_id` |
| `get_live_odds` | Current in-play moneylines, spreads, totals, and team totals for one sport |
| `get_prematch_odds` | Current pregame odds for one sport |
| `get_event` | Full current odds for one event |
| `get_prematch_lines` | Compact full-game lines for one prematch event |
| `get_drops` | Recent price drops with from/to price, drop %, and the no-vig fair price |
| `get_health` | Feed status and freshness |

All tools are read-only. The hosted server is the source of truth for tool names and schemas.

The plugin also ships a `pinnacle-odds` skill that tells the agent which tool to call, in what order.

## Notes

- Prices are decimal odds and change constantly. Responses carry `generated_at`.
- PinnWire supplies current Pinnacle prices only. It is not a multi-book scanner, a historical odds archive, or a place to bet.
- The tools take no personal data. Requests are logged with key and IP address for rate limiting.

## Docs

- MCP setup guide: https://pinnwire.com/sports-odds-mcp-server.html
- Full API reference: https://pinnwire.com/llms-full.txt
- Pricing: https://pinnwire.com/#pricing
- Server URL: https://pinnwire.com/mcp
- Support: support@pinnwire.com

## License

MIT
