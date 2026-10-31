# Installing the PinnWire MCP server

PinnWire is a remote MCP server, so there is nothing to clone, build or run locally.

1. Add this server to the MCP settings (Streamable HTTP):
   ```json
   {
     "mcpServers": {
       "pinnwire": { "type": "streamableHttp", "url": "https://pinnwire.com/mcp" }
     }
   }
   ```
2. No API key is needed: requests without a key use the shared public demo (10/min, 50/day).
3. Optional: if the user has a free PinnWire key (from https://pinnwire.com), change the URL to `https://pinnwire.com/mcp?key=THEIR_KEY`.
4. Verify by calling `list_sports`, then `get_live_odds` with `sport_id` 1 (Soccer) and `max_events` 3.
