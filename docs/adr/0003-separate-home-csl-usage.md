# ADR-0003 — Separate home: csl-usage instead of a csl-observatory boundary flip

_Created: 09-11-2026 · Status: Accepted · Decider: Dr. Mārcis Gasūns · MiMo v2.6 Pro (`mimo-v2.6-pro`) via DSH_

## Context

csl-observatory's legacy roadmap planned a "Phase E — Cologne Matomo ingest" with a "most-looked-up entries top 100" KPI, then the 2026-06-04 boundary decision scoped website usage analytics out of observatory "unless a new human decision assigns them a separate home" (`csl-observatory/docs/BOUNDARY_RULES.md:62`, `docs/DECISIONS_NEEDED.md:103`). The observatory's Paper 1 explicitly lists Matomo/top-entry analytics as out of scope. The programme here has grown to research output + public page + citable dataset — programme-sized.

## Decision

Create **csl-usage** in the `sanskrit-lexicon` org as that separate home. The csl-observatory boundary stays unchanged; its legacy Phase-E design documents are referenced as prior art.

## Consequences

- Paper 1's scope stays clean; no re-litigation of a 4-month-old deliberate decision.
- csl-usage carries its own citable identity (Zenodo releases) and its own glossary/ADRs.
- +1 repo in the org (accepted; onboarding is mechanical).
- The boundary clause's escape hatch is now exercised and can be closed as resolved.
