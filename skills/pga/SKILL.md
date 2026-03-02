---
name: pga
description: Screen products for FDA, EPA, USDA, CPSC, FCC, and other PGA (Partner Government Agency) requirements using AskRosetta. Use when checking regulatory compliance for imports.
allowed-tools: Bash, Read
argument-hint: [product description]
---

# Rosetta PGA Screening

Determine which US government agencies require clearance for an imported product. Screens against FDA, EPA, USDA, CPSC, FCC, TTB, DEA, NHTSA, and other Partner Government Agencies.

## How to Use

Extract from user input:
- Product description
- Optional: HTS code, intended use, material composition

## API Call

```bash
curl -s -X POST "https://api.askrosetta.ai/api/v1/pga" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: ${ROSETTA_API_KEY:-$ASKROSETTA_API_KEY}" \
  -d '{
    "product_description": "$ARGUMENTS",
    "hts_code": "<if known>",
    "intended_use": "<if specified>"
  }'
```

## Response Format

Present as:

**PGA Screening Result**

- **Requires PGA**: Yes/No
- **Agencies**:
  - FDA — Prior Notice required, product registration
  - EPA — TSCA certification
  - (etc.)
- **Warnings**: any flags or holds
- **Est. Processing Time**: X-Y business days

If no agencies are flagged, confirm the product appears to be exempt from PGA requirements but recommend verifying with a licensed customs broker for high-value shipments.

## Fallback

Use MCP tool `determine_pga_requirements` if API is unreachable.
