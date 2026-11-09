# ADR-0002 — Hybrid instrumentation: web statistics + server-side query-event log

_Created: 09-11-2026 · Status: Accepted · Decider: Dr. Mārcis Gasūns · MiMo v2.6 Pro (`mimo-v2.6-pro`) via DSH_

## Context

The programme's atomic unit is the QueryEvent triple {raw, normalized key, outcome hit|miss} (see CONTEXT.md). Two facts rule out page-view analytics alone:

1. Lookups are XHR calls (`getword.php?key=…`); the page URL stays put, so a page-view tracker never sees most lookups.
2. A miss returns HTTP 200 with a "not found" body (`getwordClass.php:61`), so neither page views nor status-code logs record the outcome.

Conversely, a pure server-side log has no visits/geography/referrers layer for the reporting purpose.

## Decision

Two layers, each owning what it alone can see:

- **Web statistics layer** (the university's sanctioned anonymized Matomo/RRZK service): visits, geography, referrers — the reporting and public-aggregates layer.
- **Server-side query-event log**: QueryEvent triples including misses and interface-internal lookups — the coverage-gap and search-quality layer. No JS tracker required for this half.

## Consequences

- Two sources must be reconciled in the dataset README (denominators documented).
- Forward data starts only when the maintainers deploy the change (see ASK_PACKET_COLOGNE436).
- Rejected: Matomo alone (blind to misses and AJAX lookups); custom log alone (no traffic dashboard); access-log mining alone as the permanent instrument (no outcomes, no continuity story).
