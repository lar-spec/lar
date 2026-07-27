# Changelog

All notable changes to the LAR specification, schema, and reference examples will be documented in this file.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). The proposal version follows the working paper's versioning (v0.x). Breaking changes between v0.x versions are expected — see [CONTRIBUTING.md](CONTRIBUTING.md) for posture.

This changelog distinguishes two scopes:

- **Paper-anchored.** Changes that align with the working paper (currently v4.6, May 2026) at its v0.1 Draft schema scope: three primary concerns (Identity / Current State / Operations) plus optional `catalog`, `policies`, `attestation`.
- **Exploratory (repo-side refinement past paper).** Schema fields and reference-example patterns the repository accepts that have not yet been folded into the paper. These are marked explicitly and may be revised in subsequent paper versions after community adoption signals load-bearing utility, or revised based on early feedback. Implementers using the repo schema get the full set; readers of the paper get the v0.1 Draft baseline.

## [0.1.3] — 2026-07-27 — the working paper becomes reachable from this repository

No specification, schema, or reference-example changes. The working paper is now deposited open access on Zenodo (PDF and Markdown, text verified character-identical to the SSRN version, concept DOI `10.5281/zenodo.21622424`), and this repository's three agent-facing surfaces were still pointing at the login-walled SSRN landing page, or at nothing.

- `/lar.json`: `context` gained `working_paper` (the full text, one hop, no HTML parsing) and `working_paper_doi` (the citable concept DOI). The manifest previously did not mention the paper at all, although the repository exists to implement it.
- **The text is served from `lar.md`, not from the archive.** The first attempt pointed `working_paper` at the Markdown file on zenodo.org. In the field that failed for the consumers it exists for: an agent following the chain reached the declaration and could not fetch the content, because Zenodo's anti-abuse layer restricts shared and cloud IP ranges — the networks agent fleets run on. Verified: the same URL returned 200 to a bot user-agent from a clean address and 504 from a rate-limited one, and `zenodo.org/robots.txt` itself returned 403 "unusual traffic from your network" during testing. A declared leaf on a third-party domain inherits that domain's availability posture, which the publisher neither controls nor observes; the paper's §6 says deeper material is held "within the publisher's own namespace." This is not an accusation against the archive, and it is not guesswork about its policy: Zenodo's own infrastructure tunes crawler access by user-agent allowlist, and the list has one entry. [zenodo-rdm#983](https://github.com/zenodo/zenodo-rdm/pull/983) (merged 11 Sep 2024, closing [#950](https://github.com/zenodo/zenodo-rdm/issues/950), "Implement rate-limiting for User-Agents to unblock `Googlebot`") adds an nginx map whose only named agent is `Googlebot`; every other user-agent falls to the `default ""` branch and is left to the general limits — 60 requests/minute anonymous, [per Zenodo's own API documentation](https://developers.zenodo.org/) — plus address reputation. That ceiling is reasonable for a person and negligible for a fleet sharing cloud egress. An archive is entitled to defend itself; the point is only that its defensive posture becomes the publisher's availability, silently and by default, and that search crawlers are on the list while agents are not. Zenodo stays canonical and citable via `working_paper_doi`; the reference surface serves the bytes. The trade is version drift, which the publisher can see and manage.
- `llms.txt`: the "Working paper" entry linked a README anchor rather than the paper. It now links the full text in Markdown, with the citable record beside it.
- `README.md`: the "Working paper" and "Citing this work" sections lead with the open-access Zenodo record and name SSRN as the identical-text deposit, rather than citing only the venue a reader may not be able to open.
- `.zenodo.json`: `related_identifiers` now declares `isSupplementTo` the paper's Zenodo DOI as well as its SSRN DOI, so the software-to-paper relation resolves within Zenodo. Description updated to match. *(Takes effect on this release, when Zenodo reads the file.)*

The reference surface at lar.md was updated the same day: it now hosts `/lar/working-paper.md` and declares it from its own manifest, its `llms.txt`, and `about.md`.

## [0.1.2] — 2026-07-27 — documentation and metadata only

No specification, schema, or reference-example changes. This release exists so the archived artifact carries the current documentation; implementers on 0.1.1 need change nothing.

- README: Zenodo DOI badge added (concept DOI `10.5281/zenodo.20544009`, resolves to latest release). Badge image served via `img.shields.io` rather than `zenodo.org/badge/` because GitHub's Camo proxy returns 502 when fetching from Zenodo's badge endpoint; link target (concept DOI) unchanged. ([439aece](https://github.com/lar-spec/lar/commit/439aece), [be74a6b](https://github.com/lar-spec/lar/commit/be74a6b))
- README: "Citing this work" section added with formal citations for paper (SSRN) and software (Zenodo). ([439aece](https://github.com/lar-spec/lar/commit/439aece))
- README: OKF (Open Knowledge Format, Google Cloud, June 2026) added to "Relationship to adjacent work" as a convergent, different-axis knowledge format (enterprise knowledge catalog vs publisher-to-buying-agent commerce). No priority or endorsement claim. ([d6bacae](https://github.com/lar-spec/lar/commit/d6bacae))
- README: GS1 Digital Link (ISO/IEC 18975:2024) added to "Relationship to adjacent work" as a ratified precedent for projecting human and machine views from one identifier. ([2d30634](https://github.com/lar-spec/lar/commit/2d30634))
- README: "Layered" terminology note extended to disambiguate LAR (producer-side surface) from consumer-side "agentic / multi-layer retrieval" (agentic RAG; Agentic-R, Liu et al. 2026, arXiv:2601.11888). ([1d7b983](https://github.com/lar-spec/lar/commit/1d7b983))
- README: SSRN posting date stated precisely as "public 1 June 2026 (written 19 May 2026)" — was "May 2026" — refining the 0.1.1 entry below. ([a205c7e](https://github.com/lar-spec/lar/commit/a205c7e))
- `/lar.json`: `publisher.name` corrected from "LAR Specification Working Group" to "Francesco Marinoni Moretto", `publisher.domain` from `github.com` to `lar.md`. There is no working group, and the root manifest now points at the live surface, which is itself a LAR surface. README Architecture rewritten to the tiered model used there: Discovery (precondition) → Core (Identity / Current State / Operations + policies) → Trust (Validators + Attestation, experimental) → Domain extensions. The publisher name in the 0.1.0 section below was corrected to match at the same time; the 0.1.0 and 0.1.1 artifacts themselves are unchanged and still carry the original string. ([02c9c6c](https://github.com/lar-spec/lar/commit/02c9c6c))

## [0.1.1] — 2026-06-04 — SSRN link and Zenodo archival metadata

- README: SSRN paper link added (paper made public on SSRN 1 June 2026, written 19 May 2026 — `ssrn.com/abstract=6801118`, DOI `10.2139/ssrn.6801118`). ([ea25662](https://github.com/lar-spec/lar/commit/ea25662))
- `.zenodo.json` added, enabling the GitHub–Zenodo archival integration that mints the concept DOI. ([ea25662](https://github.com/lar-spec/lar/commit/ea25662))

## Repo-side refinements past paper v4.6 — shipped in [0.1.0] ([37d59c8](https://github.com/lar-spec/lar/commit/37d59c8))

*Not a release of its own. This is the second scope declared at the head of this file: where the repository departs from the paper's Appendix A.1 v0.1 Draft. All of it shipped in the 0.1.0 tag, and it is kept separate from the `[0.1.0]` entry below, which records the paper-anchored scope.*

### Schema change — required-property reduction

- **`required` reduced from `["lar_version", "publisher", "identity", "current_state", "operations"]` to `["lar_version", "publisher", "identity"]`.** `current_state` and `operations` become optional. The previous required set carried a commerce-with-fulfillment bias that excluded valid publisher surfaces: a documentation/specification publisher (this repository) with no volatile state and no transactional operations; a static publication (a research foundation between active programs) with identity but no current state; an institutional publisher whose entire publication surface is narrative leaves (manifesto sites, academic papers as surfaces). The repository's own root `/lar.json` (added in this release, see "Self-demonstrating root surface" below) motivates the change. Vanelli and restauro both retain `current_state` and `operations` and continue to validate.

### Self-demonstrating root surface

- **`/lar.json` at the repository root** — the repository now exposes its own LAR manifest. The publisher is Francesco Marinoni Moretto; `identity` points to the README; `context` declares the specification artifacts (schema, changelog, contributing guide, both reference examples); `operations` is empty (the repo authorises no transactions); `policies` declares the license and the contributing guide. The repository treats its specification artifacts as a publication surface and exposes them through the canonical structure it documents. Eat-your-own-dogfood for the architectural claim.
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
- JSON Schema (draft-07) for the `lar.json` manifest at [`schemas/lar.schema.json`](schemas/lar.schema.json). Required fields **as specified by the paper**: `lar_version`, `publisher`, `identity`, `current_state`, `operations`. Optional fields (paper-anchored): `catalog`, `policies`, `attestation`. The schema as shipped in this tag already required only the first three — see the repo-side refinements section above.
- Protocol enumeration for the `operations` block: `ACP`, `UCP`, `MCP`, `Proprietary`. (Expanded subsequently to include `WebMCP`, `A2A`, `OpenAPI`, `Other` — see the repo-side refinements section above.)
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
