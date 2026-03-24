---
name: landed-cost
description: Calculate the total landed cost for importing a product — classify, calculate duties, and show the full breakdown.
argument-hint: "<product> <value> from <country>"
---

Run a complete landed cost calculation for the user's product:

1. **Classify** the product to get the HTS code (use `classify_hts` MCP tool or API)
2. **Calculate duty** using the HTS code (use `calculate_duty` MCP tool or API)
3. **Present** a clean duty breakdown table with base duty, Section 301/IEEPA, MPF, HMF, FTA savings, and total landed cost

Always ask for arrival date if the user has a specific shipment — tariff rates change over time.

Include CFR/USC citations for each fee component.
