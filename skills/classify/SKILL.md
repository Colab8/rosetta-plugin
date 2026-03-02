---
name: classify
description: Classify products to HTS/HS codes for customs using the AskRosetta API. Use when a user needs tariff codes, import classification, or customs analysis for any product.
allowed-tools: Bash, Read
argument-hint: [product description]
---

# Rosetta HTS Classification

Classify any product to its correct HTS (Harmonized Tariff Schedule) code using the AskRosetta multi-model AI engine.

## How to Use

When the user provides a product description (and optionally origin country, material, value), call the AskRosetta classify endpoint.

## API Call

```bash
curl -s -X POST "https://api.askrosetta.ai/api/v1/classify" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: ${ROSETTA_API_KEY:-$ASKROSETTA_API_KEY}" \
  -d '{
    "product_description": "$ARGUMENTS",
    "country_of_origin": "<extract from context or omit>",
    "value_usd": <extract from context or omit>
  }'
```

If no API key is set, try the MCP tool `classify_hts` if available.

## Response Format

Present results as:

**Classification Result**
- **HTS Code**: `XXXX.XX.XXXX` — Description
- **Duty Rate**: X.X% ad valorem
- **Confidence**: XX%
- **Source**: model used
- **Reasoning**: brief explanation

If multiple candidates are returned, show the top 3 ranked by confidence.

## Multi-Jurisdiction

If the user specifies UK, EU, CA, MX, AU, or other jurisdictions, add `"jurisdictions": ["US", "UK", ...]` to the request body. Present each jurisdiction's code separately.

## Fallback

If the API is unreachable, use the MCP tool `classify_hts` with the same parameters. If neither is available, explain the classification logic using GRI (General Rules of Interpretation) and suggest the user verify on the USITC HTS database.
