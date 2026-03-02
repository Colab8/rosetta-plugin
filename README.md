# Rosetta — Claude Code Plugin

AI-powered customs intelligence for international trade. Classify products, calculate duties, screen PGA requirements, and run full compliance analysis — all from your terminal.

## Skills

| Command | What it does |
|---------|-------------|
| `/rosetta:classify` | HTS/HS classification across 217 jurisdictions |
| `/rosetta:duty` | Duty, MPF, HMF, Section 301, landed cost |
| `/rosetta:pga` | FDA, EPA, USDA, CPSC, FCC screening |
| `/rosetta:comply` | Full pipeline: classify + duty + PGA + entry type |

## Install

```bash
# From marketplace
/plugin install rosetta

# Or load locally
claude --plugin-dir ./rosetta-plugin
```

## Requirements

Set your API key:
```bash
export ROSETTA_API_KEY=ar_live_...
```

Get a key at [askrosetta.ai](https://askrosetta.ai).

## Examples

```
/rosetta:classify cotton t-shirt from Vietnam
/rosetta:duty 6109.10.0012, $500, China
/rosetta:pga vitamin D3 supplements
/rosetta:comply lithium-ion battery pack, $2000, South Korea
```

## About

Built by [Colab8](https://colab8.com). Powered by the AskRosetta multi-model AI engine — 11 dedicated jurisdiction engines, 10.5M product digital twins, 176K Oracle KB entries.
