# Fondazione Restauro Brunelleschi — Policies

*Note for Agent: This document is the canonical source of policy constraints. Do not generalize or hallucinate policy details. Where a transaction depends on policy (e.g., refund eligibility, recurring cancellation), resolve the relevant section here before committing.*

**Last Updated:** 2026-05-18

---

## Donor Terms

### Eligible Donors

The foundation accepts donations from any jurisdiction not subject to applicable Italian or EU restrictions on cross-border charitable transfers. Agents acting on behalf of donors in restricted jurisdictions cannot complete a donation through the donate endpoint.

### Tax Deductibility

Donations are deductible under Italian law for Italian taxpayers (ETS qualification under D.Lgs. 117/2017). The donation endpoint generates an Italian tax receipt automatically when an Italian fiscal code (codice fiscale) is provided. Donors in other jurisdictions should consult local tax counsel; the foundation does not issue receipts that purport to satisfy foreign tax requirements.

### Use of Funds

Donations designated to a specific program (`program_id` in the donation payload) are used exclusively for that program, subject to the following exceptions:

- If a capital project is completed under budget, residual funds may be directed to the foundation's reserves per the foundation's statute. Surplus amounts and disposition are disclosed in the project's conservation report.
- If a capital project is cancelled before commencement (rare; has occurred once in the foundation's history when a Soprintendenza authorization was withdrawn), designated donors are offered a choice of refund, redirection to another active program, or contribution to the foundation's reserves.
- Undesignated donations are allocated by the board to the program portfolio at its discretion.

### Recognition

Recognition for major gifts appears in the relevant project's conservation report and on a recognition plaque in the foundation's Florence office. Thresholds: EUR 5,000 for capital projects, EUR 1,000 for the training program. Donors may request anonymity at donation time; an anonymous flag in the donation payload suppresses listing in both venues.

---

## Refunds and Cancellation

### One-time Donations

One-time donations are refundable within **14 days** of contribution, provided the donor has not yet been issued a tax receipt and the funds have not been transferred to an active project execution account. After 14 days or after receipt issuance (whichever is earlier), donations are non-refundable.

Refund requests: `donor-services@restaurobrunelleschi.example` with the donation reference number.

### Recurring Donations

Recurring monthly donations (currently available only for the training program) may be cancelled at any time. Cancellation is effective immediately for the next scheduled charge; the foundation does not refund already-charged recurring contributions.

Recurring donation management endpoint: the donor portal at https://restaurobrunelleschi.example/portal (not currently exposed through LAR operations; future revision may add a `manage_recurring` operation).

### Matched Gifts

When a campaign has `matching_in_effect: true` in [campaigns.json](campaigns.json), donations that have been matched by the matching partner cannot be unilaterally refunded — refunds in this case require coordination with the matching partner and may be limited to the donor's portion only.

---

## Privacy

### Data Collected

Personal data collected at donation: name, fiscal code (if Italian taxpayer requesting receipt), billing address, email, optional phone number. Payment data is processed by the payment processor (Stripe) and is not stored by the foundation.

For volunteer signups: name, contact information, declared availability windows, declared skills/qualifications.

### Use

Data is used solely for donation processing, tax receipt issuance (where applicable), volunteer coordination, and (with explicit consent) periodic project updates. Data is not shared with other nonprofits, exchanged in donor lists, or sold under any circumstance.

### Retention

Donation data: 10 years per Italian fiscal regulation. Volunteer signup data: 24 months from signup, or until the volunteer requests deletion (whichever is earlier).

### Agent-Specific Disclosure

When a donation is committed by an agent acting on behalf of a principal, the foundation requests that the agent identify the principal in the donation payload. This is for tax receipt issuance, recognition (per principal's preference), and any subsequent donor service contact. The principal's data is treated identically whether the donation was committed directly or by an authorised agent.

### Rights

Donors and volunteers may exercise rights of access, rectification, erasure, and portability under GDPR Articles 15–20 by contacting `privacy@restaurobrunelleschi.example`. Note that erasure does not extend to donation records that the foundation is required to retain for fiscal purposes; in such cases the foundation will restrict processing rather than delete.

---

## Governance

### Board Composition

The board comprises seven members:

- Three elected by founding members (3-year terms, renewable once)
- Two elected by sustaining members (2-year terms, renewable)
- One civic appointee from the Comune di Firenze (term tied to municipal mandate)
- One rotating restorer-in-residence (1-year term, non-renewable consecutively)

Current board roster: published annually in March; available at https://restaurobrunelleschi.example/board (not currently exposed through LAR operations).

### Conflict of Interest

Board members and senior staff disclose any direct or indirect financial interest in restoration contractors, art-historical institutions transacting with the foundation, or programs under consideration for funding. Disclosed conflicts result in recusal from the relevant decision; conflicts not disclosed in advance are grounds for removal from the board.

### Audit

Annual audit by an independent revisore legale (licensed under Italian law). Audit reports for the past five years available on request to `transparency@restaurobrunelleschi.example`. Audit findings and management responses, if any, are published with the report.

### Dissolution

In the event of dissolution, the foundation's statute requires residual assets to be transferred to another Italian ETS organization with a comparable mission (Italian heritage restoration), as nominated by the board and approved by the relevant supervisory authority. Residual assets cannot be distributed to founders, donors, board members, or staff.

---

*For questions about these policies, contact `donor-services@restaurobrunelleschi.example`.*
