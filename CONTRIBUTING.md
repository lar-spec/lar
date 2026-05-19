# Contributing to LAR

LAR is an early community proposal. This file describes how to engage with it.

## What this repository is

A working specification draft with reference examples. The schema, canonical filename, discovery mechanism, and protocol enumerations are open for community refinement. The repository is the venue for that refinement.

## What this repository is not

A production product. There is no implementation roadmap, no governance committee, no compliance program. LAR v0.1 is a starting point for discussion, not a finished standard.

## How to engage

**GitHub Issues.** Six templates are available, aligned with the working paper's §8 open-question categories plus two cross-cutting templates:

- **Schema refinement** (cross-cutting) — proposed edits to the JSON Schema.
- **Discovery mechanism** (Coordination subcategory) — feedback on the three discovery candidates and the canonical filename.
- **Naming and terminology** (Coordination subcategory) — including the canonical filename, schema field names, vocabulary values, and the LAR name itself.
- **Trust question** (Trust category) — liability, attestation, revocation, verification-at-the-leaf.
- **Runtime question** (Runtime category) — state management, quote validity, freshness conventions, idempotency, endpoint semantics.
- **Empirical contribution** (Empirical category) — benchmarks, retrieval-accuracy measurements, falsifiability evidence.
- **Bug report** (cross-cutting) — defects in schema, examples, or documentation.

Compatibility observations with adjacent specs (llms.txt, MCP, UCP, ACP, NLWeb, WebMCP, A2A, `.well-known/agent.json`) typically belong under Coordination — discovery or naming, depending on the angle.

**GitHub Discussions** for:
- Higher-level architectural questions
- Use case explorations
- Implementation experiences

## What kinds of contributions are welcome

- Schema edits with rationale (open an issue describing the problem before opening a PR)
- Additional worked examples for different domains (nonprofit, publisher, services)
- Corrections to the existing examples
- Documentation improvements
- Compatibility tests against other specifications

## What kinds of contributions are not in scope (yet)

- A reference implementation or validator: the schema is too early-stage for that to be useful
- Marketing materials, logo design, or branding work
- Standards-track submissions to W3C, IETF, GS1, or other bodies: that may come later, but not before the community process has settled enough to make formal submission meaningful

## Posture

This is an emerging-pattern proposal, not a settled standard. Refinement is expected. Breaking changes between v0.x versions are likely. Anyone implementing LAR before v1.0 should expect to update their implementation as community consensus evolves.

If you're interested in the underlying motivation and architectural commitments, read the working paper first. If you're interested in trying LAR on a real publisher surface, see the worked examples at `examples/ecommerce/vanelli/` (e-commerce) and `examples/nonprofit/restauro/` (heritage restoration foundation). Examples are grouped by publisher sector; additional sectors (`publisher/`, `services/`, `civic/`, `education/`) are welcome contributions.

## Process

1. Read the working paper to understand scope and architectural commitments.
2. Open an issue describing what you want to propose, refine, or report.
3. Discussion in the issue. Consensus is the goal, not unanimity.
4. If a change to the schema or examples is appropriate, a PR follows the issue discussion.
5. Refinement consensus reached during the open review period will be integrated into subsequent versions of the working paper.

## Communication style

- Direct and technically grounded
- Skeptical questions welcome
- "This is just X with a different name" is a legitimate position; the response is technical argument, not deflection
- Disagreement on naming, scope, and mechanism is expected — convergence comes from discussion, not from dismissing dissent

## Contact

For questions outside the issue tracker: francesco.marinoni.moretto@gmail.com

## License of contributions

By submitting a contribution to this repository, you agree that your contribution is licensed under the Apache License 2.0, the same license that covers the rest of the repository.
