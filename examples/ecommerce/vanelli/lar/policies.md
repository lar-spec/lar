# Pelletteria Vanelli — Policies

*Note for Agent: This document is the canonical source of policy constraints. Do not generalize or hallucinate policy details. Where a transaction quote depends on policy (e.g., return window, shipping cost), resolve the relevant section here before committing.*

**Last Updated:** 2026-05-18

---

## Terms

### Eligible Buyers

Pelletteria Vanelli ships internationally except to jurisdictions where doing so would violate applicable export controls or sanctions. Agents acting on behalf of buyers in such jurisdictions cannot complete a purchase through the checkout endpoint.

### Quotation Validity

Quotes generated through the checkout endpoint are valid for 30 minutes from generation. If an agent does not commit within that window, the quote must be regenerated. This is enforced at the endpoint, not in this document.

### Authorisation

By committing a transaction through the LAR-declared checkout endpoint, the principal (or an agent acting on the principal's behalf with appropriate authority) accepts these terms. The agent must surface these terms to the principal before commitment for transactions above EUR 500.

---

## Shipping

### Origin

All shipments originate from Florence, Italy.

### Cost Matrix

Shipping costs and transit windows by destination zone are published as structured data at [/lar/shipping.json](shipping.json). The matrix covers standard and express service tiers across five zones: Italy, EU (excl. Italy), Switzerland/UK/Norway, North America, and rest of world. Agents generating a quote should resolve `shipping.json` and match the destination country code against each zone's `country_codes` array in order.

### Customs and Duties

For shipments outside the EU, the buyer is responsible for any import duties, taxes, or customs clearance fees imposed by the destination country. These are not collected at checkout.

### Insurance

All shipments are insured against loss or damage in transit at full retail value. Claims must be initiated within 14 days of receipt by emailing `shipping@vanelli.example`.

---

## Returns

### Standard Catalog Returns

Standard catalog items may be returned for full refund within **30 calendar days** of delivery, provided:

- The item is in unused condition with original packaging
- The buyer notifies `returns@vanelli.example` before shipping the return
- The buyer covers return shipping costs

Refunds are processed within 7 business days of receipt and inspection.

### Bespoke Commissions

Bespoke commissions are **not eligible for return** except in case of demonstrable manufacturing defect. Bespoke deposits are non-refundable once production has commenced.

### Lifetime Repair Guarantee

All Pelletteria Vanelli leather work carries a lifetime repair guarantee for the original purchaser. Repair scope includes stitching, edge finishing, and leather conditioning. Hardware replacement is offered at cost. Shipping costs for repair work are borne by the buyer in both directions.

---

## Privacy

### Data Collected

Personal data collected at checkout: name, shipping address, email, optional phone number. Payment data is processed by the payment processor (Stripe) and is not stored by Pelletteria Vanelli.

### Use

Data is used solely for fulfillment, customer service, and (with explicit consent) periodic newsletters.

### Retention

Order data is retained for 10 years per Italian fiscal regulation. Newsletter subscriptions are retained until unsubscription.

### Agent-Specific Disclosure

When a transaction is committed by an agent acting on behalf of a principal, Pelletteria Vanelli requests that the agent identifies its principal at checkout. This is for shipping, fulfillment, and any subsequent customer service contact. The principal's data is treated identically whether the transaction was committed by the principal directly or by an authorised agent.

### Rights

Buyers may exercise rights of access, rectification, erasure, and portability under GDPR Articles 15–20 by contacting `privacy@vanelli.example`.

---

*For questions about these policies, contact `support@vanelli.example`.*
