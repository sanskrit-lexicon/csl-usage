# ASK PACKET — COLOGNE#436 "Matomo Statistics": enable usage measurement for the CDSL frontends

_Created: 09-11-2026 · MiMo v2.6 Pro (`mimo-v2.6-pro`) via DeepSeek Harness · for Dr. Mārcis Gasūns_
_Purpose: ready-to-post comment + one-page brief for Jim Funderburk / Dr. Dhaval Patel (+ RRZK). MG posts/forwards; agents never send._

## Part 1 — Comment for COLOGNE#436 (ready to post)

> Following up on this issue (and on the old #121 "user query statistics"): I would like to enable anonymized usage measurement for the dictionary frontends, in two small pieces:
>
> 1. **Anonymized web statistics** via the university's standard Matomo/RRZK service (the "Datenschutzhinweise zu Webstatistiken" regime: anonymized, no personal data, opt-out link in the footer). This covers visits, geography, referrers — the "is our popularity increasing?" question from #121.
> 2. **A server-side query-event log** in the web frontends: one line per lookup with the (normalized) query, dictionary, hit/miss, and an actor class (human UI / third-party API / bot). Deliberately minimal on privacy: **no IP, no cookies, no user IDs; raw query strings kept 7 days, then only k≥5-suppressed aggregates**. This is what tells us *which words* people look up and which lookups fail — directly useful for dictionary coverage and for fixing transliteration problems.
>
> Nothing about this is Google Analytics; the earlier concerns about third-party trackers do not apply. Everything runs on university infrastructure and stays inside the university's data-protection framework. The full design (including the privacy regime) is documented in the new **sanskrit-lexicon/csl-usage** repo.
>
> Two asks: (a) Jim/Dhaval — deploy the tracker include + the small logging hook when convenient; (b) RRZK — activate Matomo for this vhost. Also, separately: the site's Datenschutz/Impressum links currently 404 and should be repointed.

## Part 2 — One-page brief for Jim / Dhaval (+RRZK)

**What we want:** know what words users look up in the dictionaries, see which lookups fail, and publish anonymized aggregates (top-100 looked-up words, top misses) — useful for coverage work, search-quality fixes, and reporting.

**Why now:** nothing has been measured since Piwik was removed (2023); the old #121 ask was "not worth the trouble" then, but the design now is much lighter and fully anonymized. The estate has the analysis pipeline ready (csl-usage).

**What is deployed where (2 pieces):**

| Piece | Where | Size | Privacy |
|---|---|---|---|
| Matomo include (RRZK service) | page templates | 1 script line + footer opt-out link | University-standard anonymized regime |
| Query-event log | `getword.php` / `query.php` handlers | ~20 lines, append-only file or table | No IP/cookies/IDs; raw strings 7 days; k≥5 aggregates only |

**What we do NOT want:** no Google Analytics, no third-party trackers, no user accounts, no raw data leaving the university. Raw processing happens on the server only; published numbers count human UI lookups only (third-party API and bot traffic excluded, documented rule).

**Data-protection framing (for RRZK):** controller remains the university; the query-event log is a server-side log analogous to access logs, minimized by design (no IP, 7-day raw retention mirroring the university's own IP rule, permanent aggregates only after k≥5 suppression). Service Datenschutz notice to be updated; the current privacy links 404 and will be fixed as part of this.

## Part 3 — Tracked tasks

| # | Task | Owner | Gate |
|---|---|---|---|
| 1 | Post the COLOGNE#436 comment | MG (human) | — |
| 2 | RRZK: activate Matomo for the CDSL vhost | RRZK via Jim/Dhaval | after #1 |
| 3 | Deploy query-event log hook (spec in csl-usage) | Jim/Dhaval | after #1 |
| 4 | Fix 404 Datenschutz/Impressum links on the CDSL site | Jim/Dhaval | independent |
| 5 | Inventory existing raw logs + metrics extent (retroactive wave) | estate agent | MG provides access path |
| 6 | Update service Datenschutz notice wording | MG draft → university | with #2–3 |
