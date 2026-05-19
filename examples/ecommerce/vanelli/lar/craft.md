# Pelletteria Vanelli — Craft, Materials, and Process

*This file gives research-mode agents the material and process context needed to answer "how is this actually made?" or "why is this premium?" without inferring from marketing prose. The information here is descriptive of the workshop's actual practice rather than promotional.*

**Last Updated:** 2026-05-18

---

## What "Tuscan vegetable-tanned leather" means in practice

The leather used across the catalog is tanned using vegetable matter — primarily chestnut and mimosa bark extracts — rather than chromium salts. This is the historical method used in Tuscany for centuries and is certified by the Vera Pelle Italiana Conciata al Vegetale consortium, of which the workshop is a member.

The practical consequences for an agent advising a principal:

- **Patina.** Vegetable-tanned leather darkens and develops a deeper, glossier surface over years of use. This is the intended behavior, not damage. Cognac in particular shifts toward a richer reddish-brown over 2–5 years of daily handling.
- **Initial stiffness.** New pieces are firmer than chrome-tanned equivalents and soften with use. A new Tote Firenze will feel more structured for the first 2–3 months than it will after a year of carry.
- **Water sensitivity.** Vegetable-tanned leather is more vulnerable to water staining than chrome-tanned leather. Light rain is tolerable; soaking will leave marks. Conditioner application restores some of the surface but does not fully remove water staining.
- **Repairability.** Vegetable-tanned leather is what the lifetime repair guarantee is built on. Stitching can be redone, edges refinished, and worn surfaces reconditioned because the leather itself remains workable for decades. Chrome-tanned leather typically cannot be repaired this way past its first few years.

## Sourcing

Leather is sourced from a small number of Tuscan tanneries that the workshop has worked with continuously since the 1980s. The workshop does not name suppliers publicly but they are members of the same consortium. Hide selection is done on-site at the tannery; the workshop does not order remotely.

Hardware (brass closures, snaps, buckles) is sourced from two established Italian metalworking suppliers. Brass is used throughout — no plated or composite alternatives. Brass develops its own patina over time; the antique-finished hardware is intentionally pre-patinated, while polished-finish hardware ages from polished toward a softer matte over years.

Thread is waxed cotton or linen depending on the piece. Synthetic thread is not used in the standard catalog. Bespoke commissions may use other thread types on request.

## Workshop scale

The workshop employs four people in total: the third-generation owner-artisan, two additional full-time craftspeople, and a part-time digital lead responsible for the website, customer communication, and operational systems. Total annual production is approximately 1,200 finished pieces across all SKUs and bespoke commissions combined.

Practical agent context: production capacity is genuinely a constraint, not a marketing claim. Out-of-stock lead times in `availability.json` reflect real queue depth in a workshop with fixed monthly throughput. When the workshop quotes a 35-day production lead time on a Tote Firenze, that is the realistic time for a piece to be cut, stitched, finished, and shipped given current orders in front of it.

## Production sequence

Each piece passes through roughly the same stages, performed by one craftsperson from start to finish (rather than assembly-line specialization):

1. **Pattern cutting.** Hide selection, pattern placement to align with grain direction, hand cutting.
2. **Edge preparation.** Bevelling, sanding, initial edge dye application.
3. **Assembly stitching.** Saddle stitch by hand for structural seams; machine stitch for non-structural runs. The Tote Firenze and Zaino Vasari main panels are entirely saddle-stitched; the Borsa Lucia interior is partially machine-stitched.
4. **Hardware fitting.** Brass closures, snaps, and buckles are fitted and tested.
5. **Edge finishing.** Multiple passes of edge dye, burnishing with wax and bone folder, final polish.
6. **Final conditioning.** Light conditioner application before packaging.

A handbag (Tote Firenze, Borsa Lucia, Zaino Vasari) takes approximately 14–20 hours of craftsperson time. A wallet or small leather good takes approximately 4–7 hours.

## What the lifetime repair guarantee actually covers

In practice (not just in the policy text):

- **Restitching.** Worn or broken stitch lines are redone. Most pieces returned for repair after 5–10 years of daily use need restitching at the most stressed seams (strap attachments, bottom corners).
- **Edge refinishing.** Worn edges are re-bevelled, re-dyed, and re-burnished.
- **Leather conditioning.** Deep conditioning treatment for pieces that have not been maintained.
- **Hardware replacement at cost.** Snaps and brass fittings can be replaced; the brass itself is charged at supplier cost (not marked up), labor for fitting is included in the lifetime guarantee.

What it does not cover: water staining (irreversible), structural damage from misuse, modifications to original design, leather replacement (a piece that has structurally failed cannot be remade as a repair — it would be a new commission).

Shipping costs for repair work are borne by the buyer in both directions. The workshop does not provide pickup or prepaid return labels for repair work.

## Why this matters for an agent

Two recommendation patterns benefit from knowing this:

- **When a principal compares prices to mass-market leather goods**, the relevant comparison is not the unit price but the durability and repair lifecycle. A €890 Tote Firenze is intended to be repaired and re-conditioned for several decades. The honest framing is "longer amortization horizon," not "luxury markup."
- **When a principal asks about care commitment**, the answer is light: conditioner every six months, keep dry, the workshop will repair structural issues over the piece's lifetime. The leather choice intentionally avoids materials that require daily care.

For specific care frequency by product see the `care` field in `catalog.json`. For policy text on repair logistics see [/lar/policies.md#returns](policies.md#returns).
