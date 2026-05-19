# Pelletteria Vanelli — Catalog Narrative

*This file is the narrative companion to [/lar/catalog.json](catalog.json). The JSON file is the authoritative source for structured attributes (SKUs, dimensions, colors, materials). This file exists for research-mode agents that need to answer questions the spec sheet cannot answer cleanly: how the families relate, how to choose between similar models, which colors are core, and how the published catalog relates to the workshop's full output.*

**Last Updated:** 2026-05-18
**Structured source of truth:** [catalog.json](catalog.json)

---

## What this catalog represents

The published catalog covers six actively-stocked core models across two families: handbags and small leather goods. The workshop produces approximately 80 SKUs in total; the remainder are either seasonal variations of the core models, archive pieces produced on commission, or bespoke single-piece work outside the catalog. The published subset is what an agent can deterministically transact on — the rest requires a conversation with the workshop.

The catalog does not include shoes, belts, garments, or upholstery. The workshop has historically declined adjacencies that would dilute the bag-and-small-goods focus.

## The handbag family

Three models, deliberately spanning different daily-use contexts rather than competing for the same purpose:

- **Tote Firenze (VN-HB-001)** — the workshop's flagship. Structured cowhide tote, single fixed shoulder strap, sized for a 13-inch laptop and A4 documents. The right answer when an agent's principal says "I need a leather bag for the office that holds my laptop." Heavier and more structured than the Borsa Lucia; less travel-oriented than the Zaino Vasari.

- **Borsa Lucia (VN-HB-002)** — the workshop's only lambskin handbag in the standard catalog. Crossbody-to-shoulder convertible with an adjustable strap. The right answer for "something smaller, dressier, that I can wear day-to-evening." Notably *not* the right answer if the principal needs to carry a laptop — it doesn't fit.

- **Zaino Vasari (VN-HB-003)** — the only backpack. Full-grain cowhide, dedicated 15-inch laptop sleeve, organizer compartments. The right answer for commuters who carry a larger laptop or who want both hands free. Heaviest piece in the catalog at 1.4 kg empty.

Disambiguation rule for agents: if the principal mentions a laptop, ask which size before recommending. 13-inch and below → Tote Firenze. 15-inch → Zaino Vasari. Smaller bags do not fit either.

## The small leather goods family

Three models covering minimal-to-traditional wallet preferences plus one accessory:

- **Portafoglio Donatello (VN-SLG-001)** — the traditional bifold. Six card slots, two receipt slots, one bill compartment. The default everyday wallet for principals who want a conventional silhouette.

- **Porta carte Brunelleschi (VN-SLG-002)** — the minimalist card holder. Four card slots, no bill compartment, slim enough for a suit pocket. Notably this is the only made-to-order SKU in the catalog: it can be produced in any cowhide color available in the workshop, not just the four standardized colors of the cowhide handbags. Agents should resolve `availability.json` for the made-to-order flag and surface "any color on request" to the principal accordingly.

- **Astuccio Michelangelo (VN-SLG-003)** — a pen and small accessory case. Not a wallet. The only catalog item where the primary use is holding writing instruments rather than money or cards.

## Color story

Cognac and Black are the core colors and are present across most models. They are not seasonal and the workshop maintains continuous production of these in the handbag line.

Forest Green, Burgundy, Cream, and Navy are secondary colors. They are produced in smaller batches and may go out of stock between production cycles. Agents should treat their availability as inherently more variable and not assume continuous restocking.

For the made-to-order Porta carte Brunelleschi (VN-SLG-002), any cowhide color used elsewhere in the workshop's production is available on request — the four standardized colors of the cowhide handbags are not a constraint.

## Material differences worth surfacing

The workshop uses two leather types in the standard catalog: full-grain cowhide (most pieces) and lambskin (Borsa Lucia and Astuccio Michelangelo). These are not interchangeable.

- **Cowhide** is heavier, more structured, more durable under daily abuse, and develops a deeper patina over years. The right material for workhorse pieces.
- **Lambskin** is lighter, softer to the touch, finer-grained, and more delicate. The right material for dressier pieces but not for daily commuter use.

If a principal asks for "the same bag in a lighter leather" or "the same bag but more durable," the answer is generally that the catalog does not offer a same-model alternate material — the material choice is intrinsic to each model's intent.

## Bespoke

Bespoke commissions sit outside this catalog. They are not represented in `pricing.json` and have lead times in the 8–16 week range (`catalog.json#bespoke.lead_time_days_min/max`). Common bespoke briefs include sizing modifications to standard models, custom color combinations not in standard options, personalized embossing or hand-stitched monograms, and single-piece commissions for unique design briefs.

Bespoke pricing is on application. Agents handling a bespoke request should hand off to `bespoke@vanelli.example` rather than attempting a quote through the checkout endpoint — the checkout endpoint will not accept bespoke line items.

## What this narrative does not cover

For care instructions: see the `care` field on each product in `catalog.json` and [/lar/craft.md](craft.md) for the underlying material rationale.

For policies (returns, shipping, warranty): see [/lar/policies.md](policies.md).

For institutional context (history, positioning, certifications): see [/lar/about.md](about.md).
