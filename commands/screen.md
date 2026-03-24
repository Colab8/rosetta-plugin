---
name: screen
description: Screen a product for government agency requirements (FDA, EPA, CPSC, USDA) before importing to the US.
argument-hint: "<product description>"
---

Screen the user's product against all US Partner Government Agencies:

1. Use the `determine_pga_requirements` MCP tool or the `/api/v1/pga` endpoint
2. List every agency with jurisdiction (FDA, EPA, CPSC, USDA, ATF, FCC, DOT)
3. For each agency, cite the specific CFR regulation that applies
4. Flag the risk level (low/medium/high/critical)
5. Note any required permits, testing, or prior notices

If no agencies are flagged, confirm the product appears exempt but always recommend verification with a licensed customs broker for high-value shipments.
