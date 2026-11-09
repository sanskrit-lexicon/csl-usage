# ADR-0001 — Raw query data privacy regime

_Created: 09-11-2026 · Status: Accepted · Decider: Dr. Mārcis Gasūns · MiMo v2.6 Pro (`mimo-v2.6-pro`) via DSH_

## Context

Raw query strings are the diagnosis layer for transliteration/normalization failures (a search-quality purpose of the programme), but they can contain personal data — users paste names, emails, miscellanea. The service runs on University of Cologne infrastructure, so the university is the GDPR controller, and German data-protection practice is strict. The university's own Datenschutz keeps IPs at most 7 days (then anonymized/deleted) and runs its web statistics fully anonymized.

## Decision

1. Raw query strings are processed **on Cologne infrastructure only**; they never leave it.
2. The query-event log stores **no IP addresses, no cookies, no user IDs** — only endpoint, actor class, transliteration scheme, timestamps.
3. Raw strings are retained **7 days**, then purged; only aggregates survive.
4. Only **k≥5 small-cell-suppressed aggregates** may leave the server.
5. The service's Datenschutz notice is updated to cover the query-event log (and the currently-dead privacy links are fixed).

## Consequences

- Diagnosis of lookup failures must happen within the 7-day window (~1.5k visits/day gives ample material).
- Analysis scripts run server-side; iteration is slower than local analysis — accepted cost.
- The 7-day window mirrors the university's own IP rule, giving one defensible sentence for the data-protection notice.
- Rejected alternatives: raw 30/90 days (longer diagnosis, weaker posture); indefinite raw archive (needs explicit controller approval + records of processing); local-machine processing under a DPA (personal data on a private machine is exactly what strictness targets).
