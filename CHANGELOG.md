# Changelog

All notable changes to the LAR specification, schema, and reference examples will be documented in this file.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). The proposal version follows the working paper's versioning (v0.x). Breaking changes between v0.x versions are expected — see [CONTRIBUTING.md](CONTRIBUTING.md) for posture.

This changelog distinguishes two scopes:

- **Paper-anchored.** Changes that align with the working paper (currently v4.6, May 2026) at its v0.1 Draft schema scope: three primary concerns (Identity / Current State / Operations) plus optional `catalog`, `policies`, `attestation`.
- **Exploratory (repo-side refinement past paper).** Schema fields and reference-example patterns the repository accepts that have not yet been folded into the paper. These are marked explicitly and may be revised in subsequent paper versions after community adoption signals load-bearing utility, or revised based on early feedback. Implementers using the repo schema get the full set; readers of the paper get the v0.1 Draft baseline.

## [Unreleased]

- README: SSRN paper link added (paper made public on SSRN 1 June 2026 (written 19 May 2026) — `ssrn.com/abstract=6801118`, DOI `10.2139/ssrn.6801118`).
- README: Zenodo DOI badge added (concept DOI `10.5281/zenodo.20544009`, resolves to latest release). Badge image served via `img.shields.io` rather than `zenodo.org/badge/` because GitHub's Camo proxy returns 502 when fetching from Zenodo's badge endpoint; link target (concept DOI) unchanged.
- README: "Citing this work" section added with formal citations for paper (SSRN) and software (Zenodo).
- README: OKF (Open Knowledge Format, Google Cloud, June 2026) added to "Relationship to adjacent work" as a convergent, different-axis knowledge format (enterprise knowledge catalog vs publisher-to-buying-agent commerce). No priority or endorsement claim.
- README: GS1 Digital Link (ISO/IEC 18975:2024) added to "Relationship to adjacent work" as a ratified precedent for projecting human and machine views from one identifier.
- README: "Layered" terminology note extended to disambiguate LAR (producer-side surface) from consumer-side "agentic / multi-layer retrieval" (agentic RAG; Agentic-R, Liu et al. 2026, arXiv:2601.11888).
- README: SSRN posting date stated precisely as "public 1 June 2026 (written 19 May 2026)" (was "May 2026"); CHANGELOG line aligned.

## [Unreleased] — pre-release refinements past initial v0.1.0 draft

### Schema change — required-property reduction

- **`required` reduced from `["lar_version", "publisher", "identity", "current_state", "operations"]` to `["lar_version", "publisher", "identity"]`.** `current_state` and `operations` become optional. The previous required set carried a commerce-with-fulfillment bias that excluded valid publisher surfaces: a documentation/specification publisher (this repository) with no volatile state and no transactional operations; a static publication (a research foundation between active programs) with identity but no current state; an institutional publisher whose entire publication surface is narrative leaves (manifesto sites, academic papers as surfaces). The repository's own root `/lar.json` (added in this release, see "Self-demonstrating root surface" below) motivates the change. Vanelli and restauro both retain `current_state` and `operations` and continue to validate.

### Self-demonstrating root surface

- **`/lar.json` at the repository root** — the repository now exposes its own LAR manifest. The publisher is the LAR Specification Working Group; `identity` points to the README; `context` declares the specification artifacts (schema, changelog, contributing guide, both reference examples); `operations` is empty (the repo authorises no transactions); `policies` declares the license and the contributing guide. The repository treats its specification artifacts as a publication surface and exposes them through the canonical structure it documents. Eat-your-own-dogfood for the architectural claim.
- **`/llms.txt` at the repository root** — the discovery index pointing to the canonical artifacts and to `/lar.json`. Follows the llms.txt convention as the cross-reference discovery mechanism the repository advocates in the README's Discovery section.

### Exploratory schema additions (past paper v4.6)

These optional top-level blocks are present in the current repo schema but not in the paper's Appendix A.1 v0.1 Draft. They are demonstrated in one or both reference examples (per-block labeling below) and accepted by the schema; they may be folded into a v5 paper revision after community feedback or revised based on early adoption.

- **`context`** *(demonstrated in both Vanelli and restauro)* — Optional map of supplementary narrative (typically Markdown) leaves for research-mode agent queries the structured leaves cannot answer cleanly. Keys are publisher-chosen lowercase snake_case; values are URI references. Demonstrated in the Vanelli ecommerce example (`catalog_overview`, `craft_and_materials`) and the restauro nonprofit example (`programs_overview`, `impact_reporting`).
- **`impact`** *(demonstrated in restauro only)* — Optional URI reference to structured per-program or per-project effectiveness data. Intended for publishers declaring structured effectiveness data agents may evaluate independently of compliance or financial-health status. Typically omitted by commerce publishers; Vanelli does not currently use this block. Demonstrated in the restauro nonprofit example as `impact.json` with per-outcome `verification_status` and `evidence_quality` declarations.
- **`validators`** *(demonstrated in restauro only)* — Optional inline map of third-party trust anchors (registries, qualifications, audits, oversight bodies). Each validator record carries required `name` and `authority`, plus optional `id`, `registry_uri`, `as_of`, and `machine_queryable` boolean flag indicating whether the registry exposes a public API agents can query directly. Demonstrated in the restauro nonprofit example for RUNTS, ETS qualification, annual audit, Soprintendenza oversight, and civic board appointee. Vanelli does not currently use this block — for the standard commerce case `publisher.legal_entity_id` covers the equivalent function (LEI, GS1 GLN, local tax identifier).

### Exploratory reference-example patterns (past paper v4.6)

These conventions are demonstrated in the worked examples but not yet codified in the schema. Paper v4.6 acknowledges the `as_of` + `freshness_window_minutes` pattern as a working convention; the others remain demonstrated-but-uncodified pending community feedback.

- **`as_of` + `freshness_window_minutes`** declaration pattern on every volatile JSON file. Demonstrated in Vanelli (`availability.json` 15min, `pricing.json` 60min, `catalog.json` 1440min, `shipping.json` 1440min) and restauro (`campaigns.json` 60min, `programs.json` 1440min, `impact.json` 10080min).
- **`inventory_model` discriminator** in availability JSON (e.g., `by_color` vs `made_to_order`). Demonstrated in Vanelli's `availability.json` for the made-to-order card-holder SKU.
- **`denied_destinations` with `authority_reference` + `snapshot_date`** pattern (inline snapshot of restricted destinations plus path to the authoritative current source). Demonstrated in Vanelli's `shipping.json`.
- **`verification_status` + `evidence_quality` per-outcome declarations** in structured effectiveness data, plus a `what_this_file_does_not_claim` block surfacing claim boundaries. Demonstrated in restauro's `impact.json`.
- **`vocabularies` block** in structured catalog files declaring closed value sets (`families`, `product_types`, `fits`, `program_types`, etc.) so agents indexing across publishers can converge on the same value space. Demonstrated in both Vanelli's `catalog.json` and restauro's `programs.json`.
- **Catalog split into structured JSON + narrative MD companion** (e.g., `catalog.json` + `catalog.md` under `context`), applying §3's format-follows-purpose discipline at catalog scale. Demonstrated in Vanelli (`catalog.json` + `catalog.md`) and restauro (`programs.json` + `programs.md`).

### Reference-example additions

- Restauro example: `lar/impact.json` — six completed capital restoration projects (2020–2025) plus the training program aggregate outcomes, with `verification_status` and `evidence_quality` declared per outcome and a `what_this_file_does_not_claim` block surfacing the boundaries of the claims.
- Restauro example: `validators` block in the manifest declaring RUNTS registration, ETS qualification, annual audit, Soprintendenza oversight, and civic board appointee.
- Restauro example README updated to document both new patterns.

### Documentation alignment with the working paper

These items are not schema changes — they bring the repository's documentation into bidirectional alignment with the working paper (v4.6, May 2026). Concepts the paper articulates that the repository's docs were not carrying are lifted in.

- README expanded with a **Terminology** section (publication-surface vs. transaction-surface disambiguation per paper note 6; machine-readable vs. machine-legible per paper §3; "layered" disambiguation per paper §8).
- README expanded with an explicit **Architecture** section articulating the three-layer concern model (Identity / Current State / Operations) from paper §7 as paper-anchored scope, with the three exploratory blocks (Context / Impact / Validators) clearly distinguished as repo-side refinements past v4.6.
- README adds the paper's **§6 discipline statement** as a callout: *"The discipline of building a good LAR surface is not to design the path the agent will follow, but to remove obstacles from every path the agent might take."*
- README **Status** section adds the verification-at-the-leaf trust limit (Project Deal reference, Troy et al., Anthropic 2026) and the falsifiability criteria from paper §8.
- README **Discovery** section adds concrete `robots.txt` and `<link rel="lar">` snippets per paper §6 (previously the three mechanisms were described abstractly).
- README **Relationship to adjacent work** section adds the "two projections of one canonical knowledge graph" framing from paper §5 — the structural defence against the schema.org-replacement reading.
- README new **Open questions** section mirrors the paper's §8 four-category structure (Empirical / Coordination / Trust / Runtime).
- Issue templates restructured to align with §8 categories: `04_trust_question.md`, `05_runtime_question.md`, `06_empirical_question.md` added; `04_bug_report.md` renumbered to `07_bug_report.md`; `01_schema_refinement.md`, `02_discovery_feedback.md`, `03_naming_debate.md` retained.
- CONTRIBUTING.md updated to reflect the expanded issue-template categories.

### Paper alignment — two micro-edits applied to v4.6

For complete state awareness, the working paper has received two micro-edits, version remains v4.6 (these are corrections + honest practitioner-pattern acknowledgment, not new claims):

- Appendix A.1 protocol enum expanded to match §2 narrative and repo schema: `["ACP", "UCP", "MCP", "WebMCP", "A2A", "OpenAPI", "Proprietary", "Other"]`.
- §8 State management — one sentence appended acknowledging the reference examples' `as_of` + `freshness_window_minutes` convention.

### Reference-example domain conventions

The paper's §6 robots.txt illustration uses `example.com` (RFC 2606 reserved top-level documentation domain). The repository worked examples use `vanelli.example` and `restaurobrunelleschi.example` (RFC 2606 / IANA-reserved `.example` TLD for documentation). Both conventions are valid under RFC 2606 §3, used intentionally for different reader contexts: `example.com` reads as illustrative-snippet in a paper paragraph; the sector-named `.example` second-level domains read as fictional-but-coherent-publisher in a worked example. No reconciliation needed; documented here so the asymmetry is intentional rather than accidental.

## [0.1.0] — 2026-05-18 — initial v0.1 Draft

### Added (paper-anchored v0.1 Draft scope)

- Initial public proposal of the LAR (Layered Agentic Retrieval) specification.
- JSON Schema (draft-07) for the `lar.json` manifest at [`schemas/lar.schema.json`](schemas/lar.schema.json). Required fields: `lar_version`, `publisher`, `identity`, `current_state`, `operations`. Optional fields (paper-anchored): `catalog`, `policies`, `attestation`.
- Protocol enumeration for the `operations` block: `ACP`, `UCP`, `MCP`, `Proprietary`. (Expanded subsequently to include `WebMCP`, `A2A`, `OpenAPI`, `Other` — see Unreleased.)
- Apache 2.0 license for code, schema, and examples.

### Added (reference examples)

- Reference worked example: [`examples/ecommerce/vanelli/`](examples/ecommerce/vanelli/) — Florentine artisanal e-commerce (composite). Covers structured catalog, real-time inventory, pricing, structured shipping matrix, and `context` leaves (catalog overview, craft and materials).
- Reference worked example: [`examples/nonprofit/restauro/`](examples/nonprofit/restauro/) — Florentine heritage restoration foundation (composite). Demonstrates that LAR generalizes beyond retail: no SKUs, no inventory, no shipping; programs catalog, live campaigns, donate and volunteer-signup operations, `context` leaves (programs narrative, impact reporting).
- Examples organized by publisher sector under `examples/<sector>/<publisher>/` (`examples/ecommerce/`, `examples/nonprofit/`). Anticipates additional sectors (publisher, services, civic, education) without requiring future restructuring.
- GitHub issue templates for the feedback categories the repository explicitly invites.

### Open questions called out in v0.1

These are not omissions; they are the things the community refinement period exists to settle. See [CONTRIBUTING.md](CONTRIBUTING.md) and the working paper §8 for context.

- Discovery mechanism (three candidates enumerated in README; none selected).
- Attestation trust model (signing scope, revocation semantics, key distribution).
- Canonical filename (currently `lar.json` at `/.well-known/`; open for refinement).
- Whether `context` keys should be namespaced as the ecosystem grows.
- Standardization of the freshness-window convention (`as_of` + `freshness_window_minutes`).
- Whether the three exploratory blocks (`context`, `impact`, `validators`) should be folded into the v5 paper revision or revised based on early adoption feedback.
