# Pelletteria Vanelli — Worked Example

This directory contains a composite worked example of an LAR-published merchant surface. **Pelletteria Vanelli does not exist as a real business** — it is a composite designed to illustrate the architectural pattern, drawing on observable patterns across artisanal Italian e-commerce (third-generation family operations, sub-100 SKU catalogs, premium artisanal positioning, in-house digital teams).

## What this example illustrates

A complete LAR surface as a publisher would deploy it:

```
/.well-known/lar.json          Root manifest (this directory: lar.json)
/lar/about.md                  Institutional identity (narrative root)
/lar/catalog.json              Product catalog (structured)
/lar/catalog.md                Catalog narrative (context leaf — family overview, disambiguation)
/lar/craft.md                  Craft, materials, process (context leaf — research-mode prose)
/lar/availability.json         Real-time stock with inventory_model discriminator
/lar/pricing.json              Current pricing by SKU + indicative FX rates
/lar/shipping.json             Structured shipping cost matrix by zone
/lar/policies.md               Terms, returns, privacy, shipping narrative
```

The structure illustrates the three architectural commitments:

1. **Format follows purpose** — `lar.json` and the structured leaves (`catalog.json`, `availability.json`, `pricing.json`, `shipping.json`) are JSON because agents need deterministic parsing for joins and quotes; `about.md`, `catalog.md`, `craft.md`, and `policies.md` are Markdown because their content is narrative.

2. **Progressive disclosure** — an agent doing a spec lookup descends into `catalog.json`; an agent answering "how should I choose between these two bags?" descends into `catalog.md`; an agent answering "why is this premium?" descends into `craft.md`; an agent purchasing descends into `availability.json` + `pricing.json` + `shipping.json` + the checkout endpoint; an agent handling a complaint descends into `policies.md`. The manifest never forces all leaves on all agents.

3. **Workflow-organised hierarchy** — leaves are named by what an agent needs to do (browse catalog, recommend across the line, check availability, compute total with shipping, verify policy, explain provenance) rather than mirroring a human-navigable menu structure.

## What this example is not

- A complete merchant surface for production use. Real merchants will have larger catalogs, more granular pricing structures, and additional operational endpoints.
- A normative template. The exact field naming, file organisation, and content structure are illustrative. Different merchants will adapt LAR to their domain.
- Validated against a deployed agent ecosystem. Empirical validation against retrofit baselines is planned in a forthcoming field study (Marinoni Moretto & Antichi, 2026).

## Cross-file conventions used here

A few conventions are demonstrated that improve agent usability and that future revisions of the schema may formalize:

- **Stable SKU keys join across files.** `VN-HB-001` resolves identically in `catalog.json`, `availability.json`, and `pricing.json`. An agent composing a quote does not need fuzzy matching.
- **`inventory_model` discriminator on each SKU in `availability.json`.** Most SKUs use `"by_color"` (with `in_stock_by_color`); the made-to-order card holder uses `"made_to_order"` (with `in_stock_total` and a `color_policy`). Agents branch on the discriminator rather than sniffing field shape.
- **Single source of truth for lead times.** Production lead times live in `availability.json` only (they change with workshop load). The catalog does not duplicate them.
- **`as_of` + `freshness_window_minutes` on every volatile file.** Agents know when to refetch.
- **Structured shipping zones with explicit country codes.** `shipping.json` lists ISO 3166-1 alpha-2 codes per zone plus a `"*"` catch-all for rest-of-world, so an agent can resolve a destination deterministically.
- **Inline denied-destination snapshot with authority pointer.** `shipping.json#denied_destinations` carries the publisher's current snapshot of ineligible jurisdictions plus an `authority_reference` URL so agents have both a fast inline check and a path to the authoritative current list.
- **Indicative FX rates in `pricing.json`.** Agents can present a non-EUR estimate before commit; the binding non-EUR price is computed at the checkout endpoint.
- **Controlled vocabularies declared in `catalog.json#vocabularies`.** Closed value sets for `families`, `product_types`, and `fits` so two agents indexing the catalog converge on the same value space rather than disagreeing on freeform tokens.
- **Per-product `description` in `catalog.json`.** A short narrative summary alongside the structured attributes for research-mode agents, without duplicating institutional context that belongs in `about.md`.
- **Single source of truth for agent contact.** The address for agent operators (`agents@vanelli.example`) is declared once in `about.md`. The manifest does not duplicate it; one extra fetch is the price of canonicity.
- **`context` block for research-mode narrative leaves.** The manifest declares a `context` map pointing to `catalog.md` (catalog narrative) and `craft.md` (materials and process narrative). These complement the structured leaves: they exist to answer recommendation, disambiguation, and "why is this so" questions that structured attributes cannot answer cleanly. Publishers can add more (e.g., `care_guidance`, `history`) without schema changes — `context` accepts arbitrary lowercase-snake-case keys.

## How to read this example

Start with `lar.json` — that's what an agent fetches first. Then follow the links the agent would resolve depending on its task:

- For brand/identity context: `lar/about.md`
- For structured spec lookup: `lar/catalog.json`
- For catalog recommendation / disambiguation prose: `lar/catalog.md`
- For materials and process questions: `lar/craft.md`
- For purchase preparation: `lar/availability.json`, `lar/pricing.json`, `lar/shipping.json`
- For policy verification: `lar/policies.md`

## Notes on illustrative blocks

- **Checkout endpoint.** The manifest declares a `checkout` operation pointing to a hypothetical `https://api.vanelli.example/checkout` UCP-compliant endpoint. The example doesn't include a runnable checkout implementation — that's outside the scope of what LAR specifies (LAR is a publishing pattern; runtime protocols are concerns of UCP, ACP, MCP).
- **Attestation block.** The `attestation` object in `lar.json` carries a placeholder signature (`EXAMPLE_ILLUSTRATIVE_SIGNATURE_NOT_VERIFIABLE`) to demonstrate the field shape only. The trust model for LAR attestation is experimental and unresolved; production implementers should not treat this block as binding.
