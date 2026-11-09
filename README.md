# csl-usage — user lookup analytics for the Cologne Digital Sanskrit Dictionaries

_Created: 09-11-2026 · MiMo v2.6 Pro (`mimo-v2.6-pro`) via DeepSeek Harness · for Dr. Mārcis Gasūns_

What words do users look up in the CDSL web frontends — what we **know**, what we **can see**, what we **can share**. This repo is the "separate home" that csl-observatory's boundary decision of 2026-06-04 explicitly reserved for website usage analytics.

## Verdict (2026-11-09)

| Question | Answer |
|---|---|
| Do we know today? | **No.** No telemetry since Piwik was removed in March 2023. |
| Can we see? | **Yes.** Apache access logs contain every lookup (queries travel as GET URLs); raw logs + limited metrics are available now; historic RRZ Piwik (site 8, 2014–2017) may still hold data. |
| Can we share? | **Aggregates only** (k≥5 suppression). Raw query strings never leave Cologne infrastructure. |

Full evidence: [docs/FACT_PACK_2026-11-09.md](docs/FACT_PACK_2026-11-09.md).

## Layout

- [CONTEXT.md](CONTEXT.md) — domain glossary (QueryEvent, Miss, Actor class, …)
- [docs/adr/](docs/adr/) — the four load-bearing decisions (privacy regime, hybrid instrumentation, separate home, human-UI-only statistics)
- [docs/FACT_PACK_2026-11-09.md](docs/FACT_PACK_2026-11-09.md) — know/see/share evidence
- [docs/ASK_PACKET_COLOGNE436.md](docs/ASK_PACKET_COLOGNE436.md) — maintainer ask (COLOGNE#436), ready to post

## Hard rules (non-negotiable)

1. **Raw query strings never enter this repo** (`.gitignore` enforces; they may contain personal data).
2. **No IP addresses, no cookies, no user IDs** in the query-event log — actor classes only.
3. Raw strings are processed **on Cologne infrastructure only**; raw is purged after **7 days**.
4. Only **k≥5 small-cell-suppressed aggregates** leave the server (public page, Zenodo releases).
5. Published statistics count **human-ui actor class only** (API/bot traffic excluded; rule pre-registered).

Rights: dataset releases CC BY-SA 4.0 (matching CDSL data); code MIT. Publish-safety gate: GO, checked 09-11-2026.
