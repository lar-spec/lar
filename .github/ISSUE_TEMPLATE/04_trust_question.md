---
name: Trust question
about: Liability, provenance, attestation, revocation, or verification-at-the-leaf
title: "[trust] "
labels: ["trust", "v0.1-feedback"]
---

## Which trust question

LAR v0.1 explicitly invites refinement on three trust-related questions (working paper §8):

- **Liability and provenance.** How declarative surfaces interact with EU AI Act Article 50 (applicable 2 August 2026), Italy's Legge 34/2026, US FTC Section 5 / Operation AI Comply, and emerging analogues. Evidence a publisher can produce of what they actually authorised an agent to act upon.
- **Revocation under loss of control.** How a publisher revokes a signed surface after losing control of the domain, signing key, or publishing infrastructure. The established remedies (CRLs, OCSP, key revocation registries, Certificate Transparency append-only logs) all rely on out-of-band channels that LAR does not yet specify.
- **Verification at the leaf.** What the agent reading a deterministic surface is permitted to add, omit, or invent on its principal's behalf. The `validators` block is a partial defence against the third-party-trust gap; the editorial-behaviour gap (agent confabulation, per Project Deal, Anthropic 2026) is open.

State which question you're addressing — or whether you're naming a fourth.

## What is your proposal, evidence, or objection

[Concrete proposal, cited evidence, or structured objection.]

## Adjacent regulatory or technical references

If your contribution touches an existing regulation, standard, or case (EU AI Act, RFC 9421 HTTP Message Signatures, Web Bot Auth IETF draft, Certificate Transparency, an FTC enforcement action, etc.), name it explicitly so the discussion can ground.

## Anything else
