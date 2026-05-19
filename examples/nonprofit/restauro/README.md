# Fondazione Restauro Brunelleschi — Worked Example

This directory contains a composite worked example of an LAR-published nonprofit surface. **Fondazione Restauro Brunelleschi does not exist as a real organization** — it is a composite designed to illustrate that LAR generalizes beyond retail commerce, drawing on observable patterns across Italian heritage-restoration foundations (small board, narrow program portfolio, Soprintendenza supervision, ETS fiscal qualification, transparent overhead).

## Why a nonprofit example

LAR's first worked example ([../../ecommerce/vanelli/](../../ecommerce/vanelli/)) is an e-commerce surface. A reader could reasonably ask whether LAR is genuinely a publishing pattern for any institution or whether it's e-commerce structure with a different label.

This example exists to answer that. A heritage-restoration foundation has:

- No SKUs (programs, not products)
- No inventory or pricing (donations, not purchases)
- No shipping (no physical fulfillment)
- A different operational mix (donate, volunteer signup; no checkout)
- Different policy structure (donor terms, refunds, governance — no returns/warranty)
- Different identity and impact narrative requirements

Despite all of that, the same LAR structure works without modification:

- `lar.json` is still the manifest, with identical required fields
- `identity` still points to an institutional narrative at `about.md`
- `catalog` points to the program catalog (`programs.json`) — the schema's "product/service catalog" framing covers programs-as-services cleanly
- `current_state` carries volatile state (`campaigns.json` — live fundraising progress) — no `availability` or `pricing` here, but the slot is the same
- `context` carries research-mode narrative leaves (`programs.md` for donor-advisory prose, `impact.md` for completed-work reporting)
- `operations` carries the institution's actual transactional endpoints (`donate`, `volunteer_signup`)
- `policies` carries the institution's actual policy types (`terms`, `privacy`, `returns` — repurposed here for refund/cancellation)
- `impact` (new in this example) carries structured per-project outcome data — the slot a donor agent or DAF screening system queries to evaluate effectiveness rather than just compliance/health
- `validators` (new in this example) carries third-party trust anchors (RUNTS registration, ETS qualification, annual audit, Soprintendenza oversight, civic board appointee) so the publisher's self-declaration is cross-checkable against independent authorities
- `attestation` carries the same trust-anchor block (placeholder signature for the example)

## File structure

```
/.well-known/lar.json          Root manifest (this directory: lar.json)
/lar/about.md                  Institutional identity (narrative root)
/lar/programs.json             Program catalog (structured per-program records)
/lar/programs.md               Programs narrative (context leaf — donor advisory)
/lar/campaigns.json            Live fundraising state per program
/lar/impact.json               Structured per-project effectiveness data with verification_status & evidence_quality
/lar/impact.md                 Impact reporting narrative (context leaf)
/lar/policies.md               Donor terms, refunds, privacy, governance
```

## What this example illustrates beyond the Vanelli example

- **`current_state` is not retail-specific.** `campaigns.json` shows the slot used for live fundraising progress, days remaining, donor counts, and matching-funds state — none of which exists in an e-commerce surface.
- **`operations` can be non-commerce.** `donate` and `volunteer_signup` declared via OpenAPI rather than UCP. This demonstrates that the protocol enum (`OpenAPI`, in addition to `UCP`/`ACP`/`MCP`/etc.) genuinely supports non-commerce operations.
- **`catalog` covers programs-as-services.** The schema's `catalog` field is general enough to carry a foundation's program portfolio, not just product SKUs. Same `vocabularies` pattern, same per-item structure, same `description` for research-mode use.
- **`context` accepts domain-specific narrative leaves.** The Vanelli example uses `catalog_overview` and `craft_and_materials`. This example uses `programs_overview` and `impact_reporting`. The key namespace is publisher-chosen and adapts to what the publisher's agents actually need to explain.
- **`policies` is repurposed without schema strain.** `returns` here means refund/cancellation rather than product return — the schema field is structural (a URI to the relevant policy section), and the publisher decides what semantics that maps to.

## Cross-file conventions used here (parallel to Vanelli)

- **Stable program IDs join across files.** `RB-CHIESA-SAN-NICCOLO` resolves identically in `programs.json`, `campaigns.json`, and `programs.md`.
- **`as_of` + `freshness_window_minutes` on every volatile file.** `campaigns.json` updates hourly (60-minute window); `programs.json` updates daily.
- **Structured vocabularies declared in `programs.json#vocabularies`.** Closed value sets for `program_types`, `statuses`, `heritage_categories`.
- **Single source of truth for live state.** Per-program campaign progress lives only in `campaigns.json`, not duplicated in `programs.json` (which carries only the target and structural attributes).
- **Per-program `description` in `programs.json`** plus narrative companion in `programs.md` — the same split used between Vanelli's `catalog.json` and `catalog.md`.
- **`impact.json` with declared `verification_status` and `evidence_quality` per outcome.** Each outcome metric in `impact.json` carries an honest declaration of how it was verified (`self_reported` / `soprintendenza_reviewed` / `soprintendenza_certified`) and the quality of the underlying evidence (`internal_monitoring_only` / `annual_survey_self_reported` / `soprintendenza_post_treatment_inspection` / `independent_methodology_publication` / `library_catalog_verified`). Donor agents weighting effectiveness across alternatives can use these tags rather than treating all claimed outcomes as equivalent. The pattern intentionally surfaces gaps (the `what_this_file_does_not_claim` block lists permanence, third-party-validated cost-per-outcome, and non-respondent outcomes as things this file does NOT claim).
- **`validators` block in the manifest.** Third-party trust anchors are declared inline in the manifest so agents resolve them at first fetch, not on a second hop. Each validator record names the authority, the publisher's identifier within that authority's system, and the `registry_uri` where the claim can be cross-checked. The `machine_queryable: false` flag on the RUNTS entry honestly reports that the public registry does not yet expose a per-entity API — an agent must follow the URI to a human-facing search interface. This is the European registry-fragmentation problem made explicit rather than hidden.

## Notes on illustrative blocks

- **Operations endpoints** (`donate`, `volunteer_signup`) point to hypothetical OpenAPI-described endpoints at `api.restaurobrunelleschi.example`. The example doesn't include runnable endpoint implementations — that's outside the scope of what LAR specifies.
- **Matching partner** in `campaigns.json` for the Cappella Martelli campaign is illustrative; "Ente Cassa di Risparmio" is a placeholder name and is not intended to refer to any specific real institution.
- **Attestation block** in `lar.json` carries a placeholder signature (`EXAMPLE_ILLUSTRATIVE_SIGNATURE_NOT_VERIFIABLE`) to demonstrate the field shape only. The trust model for LAR attestation is experimental and unresolved.

## How to read this example

Start with `lar.json` — that's what an agent fetches first. The `validators` block is right there in the manifest, so trust-anchor verification happens before any further resolution. Then follow the links the agent would resolve depending on its task:

- For institutional / governance / fiscal context: `lar/about.md`
- For structured program lookup: `lar/programs.json`
- For donor advisory / program disambiguation prose: `lar/programs.md`
- For live fundraising state (matching multipliers, days remaining): `lar/campaigns.json`
- For structured per-project outcomes (effectiveness evaluation, cost-per-outcome, evidence quality): `lar/impact.json`
- For completed-work impact narrative (methodology, what the foundation does and does not claim): `lar/impact.md`
- For donor terms, refund/cancellation, privacy, governance: `lar/policies.md`
