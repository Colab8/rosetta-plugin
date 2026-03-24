---
name: duty
description: Calculate customs duties, taxes, MPF, HMF, and landed cost for imports using AskRosetta. Use when a user needs duty rates, tariff calculations, or total landed cost.
argument-hint: "<HTS code or product> <value> from <country>"
---

# Duty Calculator

Calculate complete customs duty breakdown including base duty, MPF, HMF, Section 301/IEEPA tariffs, FTA savings, and total landed cost.

## When to Use

- User asks "what's the duty on...?"
- User needs landed cost for a shipment
- User wants to compare duty rates across origins

## How It Works

Use the `calculate_duty` MCP tool with HTS code, value, and origin country.

If no HTS code is provided, first classify the product using `classify_hts`, then calculate duty.

If MCP is unavailable, call the API:

```bash
curl -s -X POST "https://api.askrosetta.ai/api/v1/duty" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: ${ASKROSETTA_API_KEY}" \
  -d '{
    "hts_code": "<code>",
    "declared_value": <number>,
    "country_of_origin": "<country>",
    "transport_mode": "<ocean|air|truck>"
  }'
```

## Important: Temporal Tariffs

Duty rates change. Ask for the **arrival date** if the user has a specific shipment — Section 301, IEEPA, and safeguard tariffs have effective dates.

## Response Format

Present as a duty breakdown table:

| Component | Amount |
|-----------|--------|
| Declared Value | $X,XXX.XX |
| Base Duty (X.X%) | $XXX.XX |
| Section 301 (China) | $XXX.XX |
| MPF (19 CFR 24.23) | $XX.XX |
| HMF (26 USC 4461) | $XX.XX |
| FTA Savings | -$XX.XX |
| **Total Duty & Fees** | **$X,XXX.XX** |
| **Landed Cost** | **$X,XXX.XX** |

Note: Landed cost = declared value + duties + fees. Does NOT include freight, insurance, or brokerage fees.
