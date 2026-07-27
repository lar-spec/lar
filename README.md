# LAR — Layered Agentic Retrieval

[![DOI](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.20544009-blue.svg)](https://doi.org/10.5281/zenodo.20544009)

**A publishing architecture for agent-native web surfaces.**

This repository hosts the open community process for **Layered Agentic Retrieval (LAR)** — a proposed publisher-side architectural pattern for declaring agent-navigable surfaces under an institution's own namespace.

## What is LAR?

LAR is a conceptual vocabulary and an initial schema draft for how publishers can structure their content so that AI agents — not just human browsers — can resolve, parse, and act on it deterministically. The core proposal is a canonical manifest at `/.well-known/lar.json` plus a workflow-organised tree of plain-text resources.

Three architectural commitments:

1. **Format follows purpose** — structured data in JSON, narrative in markdown, volatile state behind APIs.
2. **Progressive disclosure** — agents traverse only the leaves their task requires.
3. **Workflow-organised hierarchy** — surfaces are shaped by agent tasks (research / transact / verify) rather than human navigation menus.

## Terminology

A few terms recur with deliberate distinction in the working paper and this repository.

**Publication surface vs. transaction surface.** "Surface" appears in adjacent agent-commerce vocabulary (AP2's "trusted surface," OpenAI/Google's "agent surface") to denote the UI a user interacts with at transaction time. LAR uses "publication surface" in a different sense: the structured artifact an institution exposes for agent traversal — the manifest and its linked tree. The two senses are complementary rather than competing. A publication surface (LAR) is what an institution exposes; a transaction surface (AP2 / UCP / ACP terminology) is where an agent acting on a principal's behalf interacts with the user.

**Machine-readable vs. machine-legible.** *Machine-readable* describes formats a machine can deterministically parse (JSON, markdown, YAML). *Machine-legible* describes content a machine can meaningfully act upon. JSON exposing five generic product attributes is machine-readable; JSON exposing twenty content-rich attributes — provenance, occasion-fit, operational constraints — is machine-legible. LAR commits to both: machine-readable formats carrying machine-legible content.

**Layered.** "Layered architecture" is used in several adjacent senses in the agent-systems literature (Huang's seven-layer agent reference architecture, Fleming et al.'s L8/L9 communication and semantic layers, Liang's seven-layer compute model). LAR's use is narrower and structural: publisher-side institutional declarations for agents arriving without prior context, organised by workflow layer rather than by infrastructure stratum or protocol hierarchy. It is likewise distinct from consumer-side "agentic" or "multi-layer" retrieval, such as agentic RAG and learned retrievers for agentic search (Agentic-R, Liu et al., 2026; arXiv:2601.11888): those name mechanisms an agent uses to retrieve over a corpus, whereas LAR specifies how the publisher structures the surface the agent retrieves from. The two are complementary, producer-side and consumer-side of the same exchange.

## Architecture

An LAR surface is read as a short stack: each layer conditions the agent's standing to rely on the next.

**Discovery is the precondition, not a layer.** Before anything is read, the agent has to find the manifest. Three complementary mechanisms do that (see [Discovery](#discovery) below): the well-known URI `/.well-known/lar.json`, a `LAR:` directive in `robots.txt`, and a `<link rel="lar">` in the HTML head. Once found, the manifest is read top to bottom.

### Core (always present)

Identity → Current State → Operations, with `policies` governing the operations.

**Identity.** What the institution is and what it stands for: legal entity, mission, certifications, taxonomies, and the policies (return, shipping, privacy, citation, access) that govern operations. Stable; lives well in markdown and structured static files.

**Current State.** What the institution offers right now: inventory, availability, pricing, schedule, paywall status, capacity, live campaign progress. Medium follows volatility — static JSON when data refreshes daily or weekly, API endpoints when it refreshes by the hour or minute. Volatile files in the reference examples carry `as_of` + `freshness_window_minutes` so agents know when to refetch.

**Operations.** What an agent can do via the surface: purchase, subscribe, cite, reserve, donate, apply, access. Each declared operation is bound to an endpoint under a stated protocol — `ACP`, `UCP`, `MCP`, `WebMCP`, `A2A`, `OpenAPI`, `Proprietary`, or `Other`.

These are concerns, not files. A simple publisher exposes them as branches of a single static tree; a publisher at scale exposes Identity as static markdown, Current State as named API endpoints, and Operations as a declarative section in `lar.json` enumerating endpoints with their protocol bindings. Same architecture, different operational shape.

### Trust (experimental, optional)

The layer an agent consults to decide whether to rely on Core at all. Both pieces are early; most publishers carry neither today.

**Validators.** Third-party trust anchors (registries, qualifications, audits, oversight bodies) declared inline so an agent can cross-check the publisher's self-declaration against authorities. Demonstrated in the restauro example for RUNTS, ETS qualification, annual audit, Soprintendenza oversight, and civic board appointee. For US nonprofits this typically points to Candid, Charity Navigator, or IRS records; for European nonprofits to national registries (RUNTS, Charity Commission, RNA, ANBI); for commerce publishers to LEI, GS1 GLN, or consortium memberships. For the standard commerce case `publisher.legal_entity_id` covers the equivalent function, so Vanelli does not use this block.

**Attestation.** A cryptographic signature over the manifest. Documented as **experimental**: LAR v0.1 does not yet specify a trust model, signing scope, or revocation semantics, and the worked examples carry a placeholder signature for shape illustration only (see the Status section below).

### Domain extensions (optional, namespaced)

Sector-specific leaves that must not redefine Core or Trust: `catalog` (commerce), `context` (knowledge-heavy publishers), `impact` (nonprofits). Demonstrated in the worked examples — Vanelli uses `catalog` plus `context` leaves (`catalog_overview`, `craft_and_materials`); restauro uses `context` (`programs_overview`, `impact_reporting`) and `impact` (`impact.json` with per-outcome `verification_status` and `evidence_quality` declarations and a `what_this_file_does_not_claim` block surfacing the boundaries of the claims). `catalog` is paper-anchored; `context` and `impact` are exploratory extensions past the working paper's v4.6 baseline. Implementers using the repo schema get the full set; readers of the working paper v4.6 get Core as the architectural baseline. The exploratory blocks may be folded into a future paper revision after community adoption signals load-bearing utility, or revised based on early feedback.

## The discipline

> The discipline of building a good LAR surface is not to design the path the agent will follow, but to remove obstacles from every path the agent might take. The work is to expose relevant data efficiently, without forcing the agent through structure that reflects the publisher's mental model rather than the agent's task.

LAR is not a stripping exercise. Brand voice, narrative, intangibles all belong on the surface where the task requires them. The discipline is to structure richness so the agent can choose how much of it to load, not to subtract it.

## Status

**This is an early proposal, not a settled standard.**

LAR v0.1 is the version proposed in the accompanying working paper. The schema, canonical filename, discovery mechanism, and protocol enumerations are all open for community refinement. Implementers should treat the schema as experimental.

The `attestation` block in the schema is documented as **experimental** and the worked examples carry a placeholder signature (`EXAMPLE_ILLUSTRATIVE_SIGNATURE_NOT_VERIFIABLE`) for shape illustration only. LAR v0.1 does not yet specify a trust model for manifest attestation; production implementers should not rely on the attestation block until the trust model, signing scope, and revocation semantics are settled in a subsequent revision.

**Verification at the leaf.** A deterministic manifest does not, by itself, prevent the agent that reads it from confabulating about what it read. Agents acting on a principal's behalf have been observed adding, omitting, or inventing details about their principals in extended exchanges (Troy et al., "Project Deal," Anthropic, April 2026). LAR's `validators` block (third-party trust anchors) and `attestation` block (manifest signing) are partial defences; they do not address the editorial behaviour of the agent itself. Production implementers should treat LAR as one component of a trust stack, not the whole.

**Falsifiability.** The claim that LAR represents an emerging architectural pattern is testable. It would be disconfirmed by operator divergence on basic shape (manifest plus linked files plus workflow-organisation), retraction rather than expansion of publishing surfaces over time, or empirical evidence that retrofit retrieval consistently outperforms structured publication for agent task completion. Empirical benchmarking against retrofit baselines is planned in a forthcoming field study (Marinoni Moretto & Antichi, 2026).

This repository exists to:

- Host the canonical schema and reference examples
- Collect community feedback via issues
- Track refinement consensus into subsequent paper revisions

## Working paper

Marinoni Moretto, F. (2026). *Layered Agentic Retrieval: A Publishing Architecture for Agent-Native Web Surfaces.* Public 1 June 2026 (written 19 May 2026). CC BY-SA 4.0.

Open access, PDF and Markdown: [doi.org/10.5281/zenodo.21622424](https://doi.org/10.5281/zenodo.21622424) · [full text in Markdown](https://lar.md/lar/working-paper.md), served from the reference surface.
Also deposited on SSRN, identical text: [doi.org/10.2139/ssrn.6801118](https://dx.doi.org/10.2139/ssrn.6801118)

## Citing this work

**Working paper (architecture and analysis):**

Marinoni Moretto, F. (2026). *Layered Agentic Retrieval: A Publishing Architecture for Agent-Native Web Surfaces.* Zenodo. https://doi.org/10.5281/zenodo.21622424

Also deposited on SSRN with identical text: https://doi.org/10.2139/ssrn.6801118

**Reference implementation (schema and examples):**

Marinoni Moretto, F. (2026). *lar-spec/lar* [Software]. Zenodo. https://doi.org/10.5281/zenodo.20544009

Both Zenodo DOIs above are *concept DOIs* and always resolve to the latest release. To cite a specific version (e.g., for reproducibility), use the version DOI listed on the Zenodo record page.

## Repository contents

```
.
├── README.md                    This file
├── LICENSE                      Apache 2.0 (code, schema, examples)
├── CHANGELOG.md                 Notable changes per version
├── CONTRIBUTING.md              How to engage with this proposal
├── .github/
│   └── ISSUE_TEMPLATE/          Issue templates aligned to working paper §8 open-question categories
├── schemas/
│   └── lar.schema.json          JSON Schema (draft-07) for lar.json manifest
└── examples/                   Worked examples grouped by publisher sector
    ├── ecommerce/
    │   └── vanelli/             Artisanal e-commerce (Pelletteria Vanelli — composite)
    │       ├── README.md        What this example illustrates
    │       ├── lar.json         Root manifest at /.well-known/lar.json
    │       └── lar/             Linked surfaces
    │           ├── about.md     Institutional identity (narrative root)
    │           ├── catalog.json     Product catalog (structured per-SKU records)
    │           ├── catalog.md       Catalog narrative (context leaf)
    │           ├── craft.md         Craft, materials, process (context leaf)
    │           ├── availability.json  Real-time stock with inventory_model discriminator
    │           ├── pricing.json     Pricing + indicative FX rates
    │           ├── shipping.json    Structured shipping cost matrix by zone
    │           └── policies.md      Terms, returns, privacy, shipping narrative
    └── nonprofit/
        └── restauro/            Heritage restoration foundation (Fondazione Restauro Brunelleschi — composite)
            ├── README.md        What this example illustrates (and how it differs from ecommerce/vanelli)
            ├── lar.json         Root manifest at /.well-known/lar.json (includes inline validators block)
            └── lar/             Linked surfaces
                ├── about.md     Institutional identity (narrative root)
                ├── programs.json    Program catalog (structured)
                ├── programs.md      Programs narrative (context leaf — donor advisory)
                ├── campaigns.json   Live fundraising state per program
                ├── impact.json      Structured per-project outcomes with verification_status & evidence_quality
                ├── impact.md        Impact reporting narrative (context leaf)
                └── policies.md      Donor terms, refunds, privacy, governance
```

## Quick example

A minimal `lar.json` manifest:

```json
{
  "lar_version": "0.1",
  "publisher": {
    "name": "Example Merchant Srl",
    "domain": "example.com"
  },
  "identity": "/lar/about.md",
  "current_state": {
    "availability": "/lar/availability.json",
    "pricing": "/lar/pricing.json"
  },
  "operations": {
    "checkout": {
      "endpoint": "https://api.example.com/checkout",
      "protocol": "UCP"
    }
  }
}
```

See [`examples/ecommerce/vanelli/`](examples/ecommerce/vanelli/) for a fuller worked example, and [`examples/nonprofit/restauro/`](examples/nonprofit/restauro/) for a non-commerce surface (a heritage-restoration foundation with no SKUs, no inventory, no shipping — programs, campaigns, donate operation).

## Discovery

Agents arriving without prior framework knowledge can discover an LAR surface through any of three complementary mechanisms. Each reaches a different class of agent (crawler-class, HTML-rendering, llms.txt-aware); empirical observation will inform which gains traction.

**A `LAR:` directive in `robots.txt`**, alongside the existing `Sitemap:` convention:

```
User-agent: *
Allow: /
Sitemap: https://example.com/sitemap.xml
LAR: https://example.com/.well-known/lar.json
```

**A `<link rel="lar">` in the HTML `<head>` of rendered pages**, aligned with adjacent proposals such as Vercel's `<script type="text/llms.txt">` and Marro et al.'s `<link rel="agent-permissions">`:

```html
<link rel="lar" href="/.well-known/lar.json">
```

**A cross-reference from `/llms.txt`** where present.

The discovery mechanism is open for community refinement — see `.github/ISSUE_TEMPLATE/02_discovery_feedback.md`.

## Relationship to adjacent work

LAR is positioned alongside (not replacing) related initiatives in the agentic web ecosystem:

- **llms.txt** — documentation-style index, complementary to LAR's institutional declaration
- **MCP / WebMCP** — protocol layers LAR's `operations` block can bind to
- **UCP / ACP** — commerce protocols LAR's `operations` block can bind to
- **NLWeb** — conversational interface over site content, complementary
- **A2A agent cards** — agent identity, different scope from publisher manifest
- **schema.org / JSON-LD** — entity-level structured data, different organisational principle (see projection note below)
- **OKF (Open Knowledge Format)** — Google Cloud's markdown-plus-YAML-frontmatter knowledge format (published June 2026) for enterprise knowledge catalogs. Convergent with LAR on the file-based, progressively-disclosed, schema-referencing primitives, on a different consumer axis: enterprise knowledge agents rather than publisher-to-buying agents. Complementary, with no dependency in either direction.
- **GS1 Digital Link (ISO/IEC 18975:2024)** — resolves a GS1 identifier to a web resource and, through content negotiation, serves a human HTML view and a machine JSON-LD view of the same identifier from one URI. A ratified precedent, at the item-identifier level, for projecting human and machine views from one source; the agent surface generalises the move from the identifier to the institution and its operations.

LAR does not require choosing among these; it specifies the publisher-side institutional declaration layer that can reference any of them.

**A note on LAR vs. schema.org/JSON-LD entity pages.** These are best understood as two projections of the same publisher-side canonical knowledge graph. schema.org/JSON-LD projects by entity, optimising for retrieval-by-identification (*what is this entity in machine-readable form?*); LAR projects by workflow, optimising for retrieval-by-execution (*what must an agent do, and in what order, to complete a task?*). The two share infrastructure — vocabulary, identifier schemes, attestation primitives — and address different consumer behaviours. They are complementary, not competitive. A publisher with a robust canonical graph can produce both, and a sophisticated agent may consume both within the same task. LAR is not a substitute for canonical structuring; it is a workflow-shaped projection of it. A merchant who builds an LAR surface without an underlying canonical graph publishes leaf files that may be plain text and well-organised but reference inconsistent entities and produce contradictions between the LAR surface and the rest of the institution's data.

## Open questions

These are the questions LAR v0.1 explicitly invites refinement on. Issue templates in `.github/ISSUE_TEMPLATE/` are organised to match these four categories from the working paper's §8.

**Empirical.** Task-success benchmarks comparing LAR surfaces against retrofit HTML and schema.org/JSON-LD entity pages on shared agent tasks (methodological precedent: WebArena, Mind2Web). Falsifiability evidence per the conditions named in the Status section above.

**Coordination.** Manifest standardisation across adjacent specs (llms.txt, MCP, A2A agent cards, NLWeb, WebMCP, UCP, ACP, `.well-known/agent.json`). Discovery mechanism convergence among the three candidates above. Canonical filename. Naming and terminology debates. Layered-architecture vocabulary disambiguation.

**Trust.** Liability and provenance under EU AI Act Article 50 (applicable 2 August 2026), Italy's Legge 34/2026, US FTC Section 5 / Operation AI Comply, and emerging analogues. Revocation under loss of control of domain, signing key, or publishing infrastructure. Verification at the leaf — what the agent reading a deterministic surface is permitted to add, omit, or invent on its principal's behalf.

**Runtime.** State management at endpoints declared by LAR — quote validity windows, inventory locks during agent deliberation, idempotency for retried transactions, session continuity across multi-step workflows. Formalisation of the freshness-window convention (`as_of` + `freshness_window_minutes`) used in the reference examples. Integration with UCP / ACP / MCP / proprietary commerce protocols.

## Get involved

- **Issues** — six templates aligned to the four open-question categories above (Empirical / Coordination — discovery, naming / Trust / Runtime) plus cross-cutting schema-refinement and bug-report templates
- **Discussions** for higher-level architectural questions
- See [CONTRIBUTING.md](CONTRIBUTING.md) for posture and process

## License

Code, schemas, and examples in this repository are licensed under [Apache License 2.0](LICENSE).

The standalone working paper (hosted separately on SSRN) is released under CC BY-SA 4.0.

## Contact

Francesco Marinoni Moretto · francesco.marinoni.moretto@gmail.com
ORCID: [0009-0004-0096-4712](https://orcid.org/0009-0004-0096-4712)

## Self-demonstrating surface

This repository exposes its own specification artifacts as a (documentation-focused) LAR surface. The canonical structure is at [/lar.json](lar.json) with the discovery index at [/llms.txt](llms.txt). The repository is its own first reference example: it eats its own dogfood for the architectural claim it proposes. The project's domain, [lar.md](https://lar.md), is now live and is itself a LAR surface: its manifest is curl-able at [`https://lar.md/.well-known/lar.json`](https://lar.md/.well-known/lar.json), published with `publisher.domain` set to `lar.md`. The repository's specification artifacts remain under the `github.com/lar-spec/lar` namespace and serve as documentation source-of-truth; the repo's root manifest names the same publisher (`Francesco Marinoni Moretto`, `lar.md`) and stands as a working example of a documentation-publisher LAR surface.
