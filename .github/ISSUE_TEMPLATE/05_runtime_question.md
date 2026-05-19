---
name: Runtime question
about: State management, quote validity, freshness conventions, idempotency, or endpoint semantics
title: "[runtime] "
labels: ["runtime", "v0.1-feedback"]
---

## Context

LAR is a publishing pattern; it does not specify the runtime semantics of the endpoints it declares. Several runtime concerns are open (working paper §8):

- Quote generation with finite validity (e.g., the 30-minute quote window declared in the vanelli example's `policies.md`).
- Inventory locks during agent deliberation.
- Idempotency tokens for retried transactions.
- Session continuity across multi-step workflows.
- Freshness window declarations (`as_of` + `freshness_window_minutes`) — the reference examples use this pattern but it is not yet a formalised LAR convention.
- When re-reading the surface is required vs. when cached state is sufficient.
- How a surface declares which endpoints provide quote semantics vs. fire-and-forget execution.

These are protocol-level concerns (UCP, ACP, MCP, or proprietary commerce protocols handle quote and lock semantics) but their integration with LAR-declared endpoints is not formalised.

## What is your proposal

[Concrete proposal — which runtime concern, what convention, what protocol bindings.]

## Reference implementation context

If your proposal is informed by an implementation against UCP, ACP, MCP, WebMCP, or a proprietary commerce protocol, note that — the runtime questions interact with the protocol's own state model and proposals are easier to evaluate with the implementation context disclosed.

## Anything else
