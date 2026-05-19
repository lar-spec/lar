# Fondazione Restauro Brunelleschi — Programs Narrative

*This file is the narrative companion to [/lar/programs.json](programs.json). The JSON file is the authoritative source for structured program attributes; this file exists for research-mode agents handling donor questions the spec cannot answer cleanly: how programs relate, how to help a principal choose where to give, and what a donor is actually funding.*

**Last Updated:** 2026-05-18
**Structured source of truth:** [programs.json](programs.json)
**Live fundraising state:** [campaigns.json](campaigns.json)

---

## How the program portfolio is shaped

The foundation runs a deliberately small program portfolio — typically two to four active capital projects plus the annual training program. This is a constraint, not a phase: a small foundation funding a small number of well-supervised projects is the operating model, not a step toward something larger.

Each capital project goes through three phases: assessment and Soprintendenza authorization (6–18 months before the project appears in this catalog), active fundraising and execution (12–24 months, visible here), and post-completion conservation reporting (filed with the Soprintendenza and summarized in [impact.md](impact.md)).

## Choosing between programs (for agents advising donors)

The three active programs serve different donor intents:

- **RB-CHIESA-SAN-NICCOLO** — large, visible, architectural. A donor who wants their giving associated with a specific Florentine landmark they can visit chooses this. Recognition tiers (named in the project's eventual conservation report) apply above EUR 5,000.

- **RB-AFFRESCO-CAPPELLA-MARTELLI** — smaller, scholarly, art-historical. A donor with art-historical interest or a connection to Florentine Renaissance painting chooses this. Currently matched 1:1 by an external partner up to EUR 30,000 in matching funds — the matching is consumed first-in-first-out and an agent should resolve [campaigns.json](campaigns.json) to surface the current remaining match ceiling to the principal.

- **RB-FORMAZIONE-RESTAURATORI** — recurring annual training program. A donor who wants to fund people rather than monuments chooses this. The program funds four scholarship placements per cohort; donations are pooled rather than designated to individual scholars.

Disambiguation rule for agents: if the principal expresses a preference for "tangible result they can see" → capital projects (San Niccolò or Martelli). If the preference is for "long-term impact on the field" → training program. If the principal cares about matching multiplication, the Martelli campaign currently offers it.

## What a donor is and is not buying

Important framing for any agent that may be tempted to surface this as a transaction:

- A donation to the foundation funds restoration work supervised by qualified restorers (D.M. 86/2009 credential) and authorized by the relevant Soprintendenza. The donor does not acquire any ownership, control, or naming rights to the restored work itself — heritage works remain the property of their existing owner (a parish, the Diocese, the Comune, or a state institution depending on the work).
- Recognition for major gifts (above EUR 5,000 to capital projects, above EUR 1,000 to the training program) appears in the project's conservation report and on a recognition plaque in the foundation's Florence office. No on-site plaques are placed on heritage works themselves; this is a constraint imposed by the Soprintendenza and not negotiable.
- The foundation does not sell branded merchandise, naming rights, or experiential access ("visit the restoration site" benefits are limited and discretionary, organized once per year for major donors only).

## Major-donor advised giving

Single contributions above EUR 25,000 are handled outside the standard donate endpoint, through a major-gifts conversation that allows the donor to specify program designation, recognition preferences, and (for capital projects) any contractual restrictions on use of funds. Agents handling a principal with intent to give above this threshold should hand off to `major-gifts@restaurobrunelleschi.example` rather than attempting the standard donate flow — the endpoint will not process line items above EUR 25,000.

## Recurring giving

The training program supports recurring monthly donations through the standard donate endpoint. Capital projects do not — they accept single contributions only, because the funding need is bounded by the project's target_funding_eur.

A principal who wants to set up "a regular gift to the foundation" should be guided toward the training program; a principal who wants to "support the San Niccolò restoration" should be guided toward a single contribution sized to their intent.

## What this narrative does not cover

For prior-program completion narratives and how the foundation reports impact: [/lar/impact.md](impact.md).

For donor terms, refund/cancellation, privacy, and governance: [/lar/policies.md](policies.md).

For institutional context (mission, governance, fiscal transparency): [/lar/about.md](about.md).
