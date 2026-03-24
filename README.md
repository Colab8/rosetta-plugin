# Trade Compliance — Claude Plugin

AI-powered customs intelligence for international trade. Classify products to HTS codes, calculate duties and landed cost, screen government agency requirements, and run full compliance analysis.

Powered by [AskRosetta](https://askrosetta.ai) — 176K customs rulings, 30K tariff lines, 7 PGA agencies. Supports English, Spanish, and Vietnamese.

## Skills

Skills activate automatically when relevant to your conversation:

| Skill | What it does |
|-------|-------------|
| `classify` | HTS/HS classification using AI + 176K customs rulings |
| `duty` | Duty, MPF, HMF, Section 301/IEEPA, FTA savings, landed cost |
| `pga` | FDA, EPA, USDA, CPSC, FCC, ATF, DOT screening with CFR citations |
| `comply` | Full pipeline: classify + duty + PGA + entry type in one pass |

## Commands

| Command | What it does |
|---------|-------------|
| `/trade-compliance:landed-cost` | Calculate total landed cost for a product |
| `/trade-compliance:screen` | Screen a product for government agency requirements |

## Connector

This plugin connects to the **AskRosetta MCP Gateway** at `mcp.askrosetta.ai` — a Streamable HTTP MCP server providing trade compliance tools. See [CONNECTORS.md](CONNECTORS.md) for setup details.

## Install

**Cowork:**
Install directly from the plugin directory at [claude.com/plugins](https://claude.com/plugins).

**Claude Code:**
```bash
claude plugin install trade-compliance
```

## Examples

```
What's the HTS code for a stainless steel water bottle from China?
How much duty would I pay on $10,000 of ceramic tiles from Italy?
Does a dietary supplement need FDA approval to import?
Give me a full compliance report for lithium-ion batteries from South Korea, $50,000 shipment
```

## About

Built by [Colab8](https://colab8.com). Powered by the [AskRosetta](https://askrosetta.ai) trade compliance engine.
