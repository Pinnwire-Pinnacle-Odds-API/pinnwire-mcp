---
name: pinnacle-odds
description: Get current Pinnacle sports betting odds, recent price drops and no-vig fair prices through the PinnWire MCP tools. Use when the user asks for live or prematch odds, moneylines, spreads, totals, dropping odds, line movement, fair/implied probabilities, or a sharp reference price for +EV or arbitrage checks.
---

# Pinnacle odds with PinnWire

PinnWire's MCP server (`pinnwire`) exposes 7 read-only tools. All prices are decimal odds.

## Workflow

1. If the sport id is unknown, call `list_sports` (13 sports; does not use quota). Soccer is 1, Tennis 2, Basketball 3, Hockey 4, Football 5, Baseball 6.
2. Pull a board:
   - in-play: `get_live_odds` with `sport_id` (use `max_events` to keep it small)
   - upcoming: `get_prematch_odds` with `sport_id`
3. Drill into one match with `get_event` (full detail) or `get_prematch_lines` (compact full-game lines; optional `market_type`: money_line | spreads | totals | team_total).
4. For movement, call `get_drops` (`mode`: live | prematch, `min_drop_pct`, `sport_id`, `limit`). Each drop has from/to price, drop % and `nvp`, the no-vig fair price. Fair implied probability = 1 / nvp.
5. `get_health` reports feed freshness (`last_odds_update_seconds_ago`).

## Rules

- Prices move constantly; quote `generated_at` and say the odds are current as of that time.
- PinnWire supplies current Pinnacle prices only: it is not a multi-book scanner, a historical archive or a place to bet.
- `nvp` is an estimate of the fair price, not a guarantee.
- On a rate-limit error, relay the message: the free demo is shared. A free personal key (100 requests/day, no card) is at https://pinnwire.com; add it as `?key=YOUR_KEY` on the server URL.
