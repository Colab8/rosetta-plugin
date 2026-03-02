---
name: comply
description: Run full import compliance analysis — classify, duty, PGA, entry type, and declaration readiness in one shot using AskRosetta. Use for end-to-end import analysis.
allowed-tools: Bash, Read
argument-hint: [product description, value, origin]
---

# Rosetta Full Compliance Analysis

Run the complete Rosetta pipeline: HTS classification, duty calculation, PGA screening, entry type recommendation, and declaration readiness check — all in one call.

## How to Use

Extract from user input:
- Product description (required)
- Declared value in USD (required)
- Country of origin (required)
- Optional: destination state, transport mode, intended use, material

## API Call

```bash
curl -s -X POST "https://api.askrosetta.ai/api/v1/analyze" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: ${ROSETTA_API_KEY:-$ASKROSETTA_API_KEY}" \
  -d '{
    "product_description": "<description>",
    "declared_value": <number>,
    "country_of_origin": "<country>",
    "destination_state": "<state>",
    "transport_mode": "<ocean|air|truck>",
    "intended_use": "<if specified>"
  }'
```

## Response Format

Present as a structured compliance report:

---
**ROSETTA COMPLIANCE REPORT**

**1. Classification**
- HTS: `XXXX.XX.XXXX` — Description
- Confidence: XX% | Source: model

**2. Duty & Fees**
| Component | Amount |
|-----------|--------|
| Base Duty (X.X%) | $XXX.XX |
| MPF | $XX.XX |
| HMF | $XX.XX |
| **Total** | **$X,XXX.XX** |
| **Landed Cost** | **$X,XXX.XX** |

**3. PGA Requirements**
- FDA: Required / Not required
- EPA: Required / Not required
- Other: ...

**4. Entry Type**
- Recommended: Type XX — Name
- Section 321 eligible: Yes/No

**5. Declaration Readiness**: READY / NEEDS ATTENTION
- Missing documents: (list)
---

## Fallback

If the `/api/v1/analyze` endpoint is unreachable, chain the individual calls:
1. `/rosetta-classify` to get HTS code
2. `/rosetta-duty` with the HTS code
3. `/rosetta-pga` for agency screening

Or use MCP tool `analyze_product` if available.
