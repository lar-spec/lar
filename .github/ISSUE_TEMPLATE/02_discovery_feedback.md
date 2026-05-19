---
name: Discovery mechanism feedback
about: Comment on or propose changes to how agents discover an LAR surface
title: "[discovery] "
labels: ["discovery", "v0.1-feedback"]
---

## Context

Discovery is one of the most contested open questions in v0.1. The README enumerates three current candidates:

- A `LAR:` directive in `robots.txt`, analogous to `Sitemap:`
- A `<link rel="lar">` element in the HTML `<head>` of rendered pages
- A cross-reference from `/llms.txt` where present

This template is for proposals, objections, or compatibility observations about discovery.

## What is your proposal or objection

If proposing a mechanism: describe it and why it's preferable to the candidates above.

If objecting to a candidate: which one, and on what grounds (technical, ecosystem-fragmentation, compatibility, operational cost for publishers).

If observing compatibility: how does the candidate interact with [adjacent spec — e.g., llms.txt, robots.txt, a CDN/edge constraint, an existing crawler convention]?

## Implementation considerations

Cost to publishers (time, infrastructure, tooling). Cost to agents (discovery latency, fallback chain complexity). Compatibility with existing crawler/agent conventions.

## Precedent

Is there a related discovery mechanism in another spec or ecosystem that informs your proposal?

## Anything else
