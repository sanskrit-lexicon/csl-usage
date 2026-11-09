# ADR-0004 — Published statistics count human-ui only

_Created: 09-11-2026 · Status: Accepted · Decider: Dr. Mārcis Gasūns · MiMo v2.6 Pro (`mimo-v2.6-pro`) via DSH_

## Context

`getword.php` is a public CORS/JSONP API that third-party pages deep-link; crawlers hit the frontends continuously. So requests ≠ users: raw traffic is polluted by api-3rd-party and bot classes. The research-output purpose requires this to be a pre-committed rule, not a later judgement.

## Decision

1. Every QueryEvent carries an **actor class** — `human-ui` | `api-3rd-party` | `bot` — assigned **at capture** from endpoint, referrer and user-agent classes.
2. **Published statistics count human-ui only.** The exclusion rule is pre-registered in every dataset README.
3. The same classifier runs **post-hoc** on the retroactive wave (historical logs carry UA + referrer).
4. Total-request figures may be shown alongside only when clearly labelled as all-traffic.

## Consequences

- Published "top looked-up words" are defensible as human lookup behaviour.
- Totals are lower than raw traffic — stated openly as a methodology choice, not hidden.
- Classification heuristics live in the dataset README with their known limits.
- Rejected: post-hoc-only filtering (post-hoc bias risk in a paper); publishing all requests labelled (polluted headline numbers); gating the public API with keys (breaks existing third-party deep links).
