# PulsePanda MCP server

A hosted (remote) [Model Context Protocol](https://modelcontextprotocol.io) server for [PulsePanda](https://pulsepanda.dev), the website and product analytics platform with session replay, heatmaps, funnels, surveys, feedback, a feature voting board, a help desk and Google Search Console / Bing Webmaster Tools data.

Connect Claude, ChatGPT, Claude Code, Cursor, VS Code or any MCP client, and your assistant can query your analytics and search data and manage forms, surveys, your roadmap and help desk conversations, all within the scopes you approve.

- **Endpoint:** `https://api.pulsepanda.dev/mcp` (Streamable HTTP)
- **Auth:** OAuth 2.1 with PKCE and dynamic client registration. Sign in with your PulsePanda account and approve the scopes. There are no API keys to copy.
- **Price:** included on every PulsePanda plan, including the free plan
- **Docs:** https://pulsepanda.dev/features/connect-your-ai

This repository holds documentation and client configuration only. The server itself is hosted by PulsePanda, so there is nothing to install or run.

## Connect

You need a PulsePanda account with at least one site ([sign up free](https://app.pulsepanda.dev)).

**Claude (claude.ai / desktop):** Settings → Connectors → Add custom connector, then use the URL `https://api.pulsepanda.dev/mcp`.

**ChatGPT:** add a connector with the URL `https://api.pulsepanda.dev/mcp`.

**Claude Code:**

```sh
claude mcp add --transport http pulsepanda https://api.pulsepanda.dev/mcp
```

**Cursor / VS Code:** use the one-click install buttons in PulsePanda under Site settings → AI Connections, or add it to your MCP config:

```json
{
  "mcpServers": {
    "pulsepanda": {
      "url": "https://api.pulsepanda.dev/mcp"
    }
  }
}
```

The first time a client connects, a browser window opens so that you can sign in to PulsePanda and approve the requested scopes. You can see and revoke connections at any time under Site settings → AI Connections.

## Tools

**Analytics**
`site_report`, `paths`, `retention`, `intent`, `errors_report`, `revenue_report`, `funnel_report`, `heatmap_summary`, `query_sessions`, `list_users`, `get_events`, `list_segments`, `list_goals`, `list_alerts`, `get_site_audit`

**Search: Google Search Console and Bing Webmaster Tools**
- `search_connections`: which providers are connected
- `search_overview`: clicks, impressions, CTR and average position against the previous period
- `search_breakdown`: top queries, pages, countries, devices, or query/page pairs
- `search_opportunities`: striking-distance queries (positions 11–20), low-CTR pages, impressions with no clicks, and decaying pages
- `search_insights`: the current insights generated after each sync
- `search_landing_pages`: landing pages with search clicks and position joined to on-site bounce rate, rage clicks, errors and conversions

**Feedback and roadmap**
`list_feedback`, `list_surveys`, `get_survey`, `create_survey`, `update_survey`, `list_survey_responses`, `list_forms`, `get_form`, `create_form`, `update_form`, `list_form_submissions`, `list_features`, `create_feature`, `update_feature`

**Help desk**
`list_conversations`, `get_conversation`, `get_conversation_context`, `find_related_conversations`, `reply_to_conversation`, `update_conversation`, `search_contacts`, `crm_report`, `list_kb_articles`, `get_kb_article`

**Setup**
`list_sites`, `get_sdk_snippet`, `get_embed_snippet`, `define_custom_event`, `list_event_definitions`, `delete_event_definition`, `create_funnel`, `list_funnels`, `delete_funnel`, `get_announcement`, `update_announcement`, `stop_announcement`, `get_consent_config`, `update_consent_config`, `list_cookies`, `add_cookie`, `delete_cookie`, `list_tutorials`, `get_tutorial`, `get_plan`

## Example prompts

- "Which queries rank 11–20 on Google for my site, and how do visitors from those landing pages behave?"
- "Where do people drop off in my signup funnel this month? Show me sessions from the biggest drop."
- "Summarize this week's survey responses and feedback messages and add the top request to the roadmap."
- "Which pages had the most JavaScript errors in the last 7 days?"

## Security

- Every connection is approved by you in the browser, and you can revoke it at any time.
- Scopes are read or write per area, and your assistant only sees the data your own PulsePanda account can see.
- Workspace roles apply: if an admin hasn't given you access to a module, the MCP tools for it refuse as well.

## Support

Questions or problems: https://pulsepanda.dev/support
