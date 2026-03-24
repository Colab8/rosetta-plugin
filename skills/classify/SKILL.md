---
name: classify
description: Classify products to HTS/HS codes for customs using AskRosetta. Use when a user needs tariff codes, import classification, or customs analysis for any product.
argument-hint: "<product description> [from <country>]"
---

# HTS Classification

Classify any product to its correct HTS (Harmonized Tariff Schedule) code using the AskRosetta engine — AI reasoning over 176K customs rulings and 22.8K CBP specification chunks.

## When to Use

- User asks "what's the HTS code for...?"
- User needs to classify a product for import
- User wants tariff information for a product

## How It Works

Use the `classify_hts` MCP tool with the product description and optional country of origin.

If the MCP tool is unavailable, call the API directly:

```bash
curl -s -X POST "https://api.askrosetta.ai/api/v1/classify" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: ${ASKROSETTA_API_KEY}" \
  -d '{
    "product_description": "<description>",
    "country_of_origin": "<country>",
    "material": "<material if known>"
  }'
```

## Ask for Details

Classification accuracy improves dramatically with:
- **Material composition** (cotton, polyester, stainless steel, etc.)
- **Intended use** (retail, industrial, personal)
- **Country of origin** (affects duty programs like USMCA)

If the user gives a vague description, ask before classifying.

## Response Format

**Classification Result**
- **HTS Code**: `XXXX.XX.XXXX` — Description
- **Duty Rate**: X.X% ad valorem
- **Confidence**: XX%
- **Reasoning**: brief explanation of why this code applies

If multiple candidates, show the top 3 ranked by confidence.

## Multi-Jurisdiction

Add `"jurisdictions": ["US", "UK", "EU"]` to the request body for cross-border classification. Present each jurisdiction's code separately.
