---
name: duty
description: Calculate customs duties, taxes, MPF, HMF, and landed cost for imports using AskRosetta. Use when a user needs duty rates, tariff calculations, or total landed cost.
allowed-tools: Bash, Read
argument-hint: [HTS code or product, value, origin country]
---

# Rosetta Duty Calculator

Calculate complete customs duty breakdown including base duty, MPF, HMF, Section 301/232 tariffs, and total landed cost.

## How to Use

Extract from user input:
- HTS code (or classify first using `/rosetta-classify`)
- Declared value (USD)
- Country of origin
- Optional: destination state, transport mode (ocean/air/truck)

## API Call

```bash
curl -s -X POST "https://api.askrosetta.ai/api/v1/duty" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: ${ROSETTA_API_KEY:-$ASKROSETTA_API_KEY}" \
  -d '{
    "hts_code": "<code>",
    "declared_value": <number>,
    "country_of_origin": "<country>",
    "destination_state": "<2-letter state code>",
    "transport_mode": "<ocean|air|truck>"
  }'
```

If no HTS code is provided, first classify the product, then calculate duty.

## Response Format

Present as a duty breakdown table:

| Component | Amount |
|-----------|--------|
| Declared Value | $X,XXX.XX |
| Base Duty (X.X%) | $XXX.XX |
| MPF (0.3464%) | $XX.XX |
| HMF (0.125%) | $XX.XX |
| Section 301 (if applicable) | $XXX.XX |
| **Total Duty & Fees** | **$X,XXX.XX** |
| **Landed Cost** | **$X,XXX.XX** |

Note Section 321 eligibility ($800 de minimis threshold).

## Fallback

If the API is unreachable, use MCP tool `calculate_duty`. If neither available, calculate manually: base duty = value * rate, MPF = value * 0.003464 (min $31.67, max $614.35 for formal entries), HMF = value * 0.00125 (ocean only).
