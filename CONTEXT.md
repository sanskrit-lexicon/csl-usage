# CONTEXT — csl-usage glossary

_Created: 09-11-2026 · MiMo v2.6 Pro (`mimo-v2.6-pro`) via DeepSeek Harness_

Glossary only. No implementation details; decisions live in `docs/adr/`.

**QueryEvent** — the atomic record: one lookup attempt in a CDSL frontend. Carries a raw query, a normalized key, a lookup outcome, an actor class, and a timestamp.

**Raw query** — the string exactly as the user typed it, together with its input scheme (transliteration encoding). Potentially personal data; short retention by design.

**Normalized key** — the internal canonical form of a query after transliteration conversion and cleanup. The reporting unit: "words users look for" means normalized keys with counts.

**Lookup outcome** — `hit(headword)` or `miss`, per lookup attempt.

**Hit** — the query resolved to at least one headword in the dictionary searched.

**Miss** — the query resolved to nothing in the dictionary searched. A first-class signal: the coverage-gap gold.

**Actor class** — who issued the lookup: `human-ui` (a person using the web interface), `api-3rd-party` (an external site or tool using the public lookup API), `bot` (crawler/automaton). Assigned at capture time.

**Dictionary version** — the state of a dictionary at the time of a lookup; outcomes are defined against it, not against today's data.

**Aggregate** — counts of normalized keys (with outcomes), after small-cell suppression. The only class of data that leaves Cologne infrastructure.

**Small-cell suppression** — dropping counts below k=5 before anything is shared, so no rare query can be singled out.

**Retroactive wave** — the one-shot analysis of historical server logs and historical metrics, yielding dataset v1.

**Forward capture** — continuous collection going forward via the query-event log and the web-statistics layer.

**Query-event log** — the server-side ledger of QueryEvents; the layer that records misses and interface lookups that page-view statistics cannot see.

**Web statistics layer** — the university's sanctioned anonymized traffic statistics (visits, geography, referrers).

**Published statistic** — any number that leaves the team: the public page or a dataset release. Always human-ui only, always k≥5 suppressed.
