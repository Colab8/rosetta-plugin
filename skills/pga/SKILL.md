---
name: pga
description: Screen products for FDA, EPA, USDA, CPSC, FCC, and other government agency requirements using AskRosetta. Use when checking regulatory compliance for US imports.
argument-hint: "<product description>"
---

# PGA Screening

Determine which US Partner Government Agencies (PGA) require clearance for an imported product. Screens FDA, EPA, USDA, CPSC, FCC, ATF, DOT, and others — with specific CFR regulation citations.

## When to Use

- User asks "does X need FDA approval?"
- User wants to know regulatory requirements for an import
- User is checking if a product needs special permits or testing

## How It Works

Use the `determine_pga_requirements` MCP tool with the product description.

If MCP is unavailable:

```bash
curl -s -X POST "https://api.askrosetta.ai/api/v1/pga" \
  -H "Content-Type: application/json" \
  -H "X-API-Key: ${ASKROSETTA_API_KEY}" \
  -d '{
    "product_description": "<description>",
    "hts_code": "<if known>",
    "intended_use": "<if specified>"
  }'
```

## Shipments by international mail (US)

If it is not clear whether the shipment arrives by international mail, ask.

**Postal informal entry**
- For each eligible shipment not exceeding $2,500 in value which is to be delivered by the Postal Service, a party with the right to make entry must transmit the informal mail entry (19 CFR 145.12(b)(1)).

**Formal entry rules**
- Formal entry is required for any mail shipment subject to the requirements of another government agency (19 CFR 145.12(a)(2)(v)).
- Formal entry is required for merchandise subject to duties under Chapter 98 or 99 HTSUS, or claiming duty-free treatment under Chapter 98 HTSUS or a Free Trade Agreement (19 CFR 145.12(a)(2)(vi)).
- Formal entry is also required, among other cases, for mail importations over $2,500 (with the exceptions listed there), for merchandise under an absolute or tariff-rate quota, and for merchandise subject to antidumping or countervailing duties (19 CFR 145.12(a)(2)(i)–(iii)).
- Compliance date for (v) and (vi): January 20, 2027 (91 FR 66638).
- At the end of the delayed compliance window, filers may choose formal entry or participate in the Entry Type 13 test for eligible shipments (91 FR 66638).

**Entry Type 13 test (CBP)**
- Available for international mail shipments valued at $2,500 or less, filed electronically in ACE (91 FR 66707; 91 FR 38007).
- For test participants, the formal entry requirements in 19 CFR 145.12(a)(2)(v) and (vi) are waived (91 FR 38007, section IV).
- The test commenced on September 22, 2026 (91 FR 66707).
- Shipments subject to PGA data requirements must transmit the additional data those requirements mandate (91 FR 38007).
- Since October 22, 2026, CBP temporarily accepts an entry type 13 not accompanied by complete electronic PGA data. CBP will announce the end of this in a future Federal Register notice (91 FR 66707).
- Shipments subject to AD/CVD or quotas remain ineligible for informal entry under the test (91 FR 38007).

**Alcohol and tobacco**
- Formal entry is required (19 CFR 145.12(a)(2)(iv)).
- Alcoholic beverages are nonmailable, with certain exceptions, and when imported in the mails are subject to seizure and forfeiture (19 CFR 145.54(a); see 18 U.S.C. 1716(f)).
- Cigarettes and smokeless tobacco are nonmailable, with the exceptions in 18 U.S.C. 1716E(b) (18 U.S.C. 1716E).

**FDA — food by mail**
- Beginning October 1, 2026, prior notice includes the name of the mail service and the mail tracking number (21 CFR 1.281(b)(10)).

**CPSC — finished products by mail**
- For finished products manufactured outside the United States and imported by mail, the certifier must enter the certificate data elements into CPSC's Product Registry before arrival (16 CFR 1110.13(a)(1)).

**When answering**
- Cite the source for each rule you apply.
- Say these are the rules as published through November 2026, and the user should check the Federal Register for later changes.

## Response Format

**PGA Screening Result**

- **Requires PGA clearance**: Yes/No
- **Agencies**:
  - FDA — Prior Notice required (21 CFR 1.276), product registration
  - EPA — TSCA certification (15 USC 2601)
  - CPSC — Testing required (16 CFR 1500)
  - (etc.)
- **Risk Level**: Low / Medium / High / Critical
- **Warnings**: any holds or flags

Always include CFR citations — users need them for compliance records.

If no agencies are flagged, confirm the product appears exempt but recommend verifying with a licensed customs broker for high-value or novel product shipments.
