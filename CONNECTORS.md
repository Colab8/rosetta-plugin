# Connectors

This plugin connects to the **AskRosetta MCP Gateway** — a Streamable HTTP MCP server providing trade compliance intelligence tools.

## AskRosetta (`askrosetta`)

| Field | Value |
|-------|-------|
| Type | HTTP MCP Server |
| URL | `https://mcp.askrosetta.ai/mcp` |
| Auth | OAuth 2.1 (PKCE) or Bearer token |
| Tools | classify_hts, calculate_duty, determine_pga_requirements, analyze_product, search_trade_intel |

### Setup

1. When you install this plugin, Claude will prompt you to connect to the AskRosetta MCP server
2. Authorize via OAuth (redirects to askrosetta.ai) or enter your API key as a Bearer token
3. Tools become available immediately

### Available Tools

- **classify_hts** — Classify products to 10-digit US HTS codes
- **calculate_duty** — Calculate duties, fees, and landed cost
- **determine_pga_requirements** — Screen for FDA/EPA/CPSC/USDA requirements
- **analyze_product** — Full pipeline: classify + duty + PGA + entry type
- **search_trade_intel** — Search 176K customs rulings and trade intelligence

### Get an API Key

Visit [askrosetta.ai](https://askrosetta.ai) to create a free account and get an API key.
