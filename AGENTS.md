# CLAUDE.md — csl-usage

<!-- hyperresearch: not applicable here; this is a measurement-pipeline repo, not a research vault -->

## What this repo is

User lookup analytics for the Cologne Digital Sanskrit Dictionaries (CDSL): what words users look up, which lookups miss, and anonymized published aggregates. Created 09-11-2026 as the "separate home" reserved by csl-observatory's 2026-06-04 boundary decision. Design record: `docs/FACT_PACK_2026-11-09.md`, `docs/adr/`, `CONTEXT.md`.

## Hard rules

1. **Raw query strings NEVER enter this repo** (`.gitignore` enforces; personal-data risk). Raw is processed on Cologne infrastructure only, purged after 7 days — ADR-0001.
2. **No IPs, no cookies, no user IDs** anywhere in query data.
3. Only **k≥5 small-cell-suppressed aggregates** are committed or published.
4. Published statistics count **human-ui actor class only** — ADR-0004; the exclusion rule is pre-registered in every dataset README.
5. Model provenance in durable output: tier + exact version (e.g. "Sonnet 5 (claude-sonnet-5)").

## Layout

- `CONTEXT.md` — domain glossary (glossary only; no implementation details)
- `docs/adr/` — accepted decisions (0001 privacy regime · 0002 hybrid instrumentation · 0003 separate home · 0004 human-ui-only stats)
- `docs/FACT_PACK_2026-11-09.md` — the know/see/share evidence
- `docs/ASK_PACKET_COLOGNE436.md` — maintainer ask; deployment is by Jim Funderburk / Dr. Dhaval Patel (+RRZK), never by us
- `tools/` — analysis pipeline (runs ON Cologne infra; only aggregate outputs land here)
- `data/` — aggregate outputs only (never raw)

## How to run

No local service. Analysis scripts are deployed to the Cologne server and run there (ADR-0001); this repo holds the scripts, the specs, and the aggregate results. The forward capture depends on the maintainer deployment in ASK_PACKET_COLOGNE436.

## CI

Org baseline (dependabot, CodeQL, pre-commit) via `cologne_batch_deploy.py`. Any pipeline script added here must have an offline test with fixture data (no network, no real queries).

## Conventions

- Dated doc headers (DD-MM-YYYY) with model provenance line.
- GitHub blob URLs for cross-repo references; the vocabulary in `CONTEXT.md` is canonical — challenge terms that drift from it.
- Outcomes (`hit`/`miss`) are defined against the **dictionary version of the time**, never against today's data.

Mirror of this file: `AGENTS.md`.
