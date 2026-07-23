# Topic Hub — A/B/C Structure Test Prototypes

Three prototype variants of the **Women & Gender** topic hub for the deployment A/B/C test.

**Base = Zafri's LIVE hub.** All copy — the "Where Yaqeen Stands" statement, Key Takeaways,
the 5 vetting steps, all 6 scholar bios + titles, the 8 FAQ Q&As, the 8 papers, 2 blogs, 4
videos, Explore tiles, and Related hubs — is pulled **verbatim from the live page**
(`/research-hubs/women-and-gender`, fetched July 2026). The **format** is the clean,
self-contained single-file prototype style of the original POC (easy to open, review, and
reorder). It is **not** built on the older local prototype.

The three arms share an **identical component set, copy, and brand** — they differ **only in
section order**, so any lift is attributable to structure alone (not content).

## The three arms

| Arm | Name | Section order (top → bottom) | Hypothesis |
|-----|------|------------------------------|------------|
| **A** | Frame & trust first *(control)* | Hero → Where Yaqeen Stands → Key Takeaways → Vetting → Scholars → FAQ → Papers → Blogs → Videos → Explore → Related | Mirrors Zafri's current live build — the baseline to beat. |
| **B** | Answer-first *(GEO / skimmer)* | Hero → **Key Takeaways → FAQ** → Where Yaqeen Stands → Papers → Blogs → Videos → Scholars → Vetting → Explore → Related | Lead with the quotable, answer-ready blocks. Instant value for skimmers + clean liftable answers high where AI engines / snippets weight them. Tests "FAQ at top vs. middle." |
| **C** | Path-to-depth *(repository / journey)* | Hero → Key Takeaways → **Papers** → FAQ → Scholars → Vetting → Where Yaqeen Stands → Blogs → Videos → Explore → Related | Funnel people into the papers (persona → topic → paper). Surface research high to drive click-through — the real conversion. |

Files:
- `women-and-gender-A-control.html`
- `women-and-gender-B-answer-first.html`
- `women-and-gender-C-path-to-depth.html`
- `build_abc_variants.py` — regenerates all three from one content source (edit once, rebuild all)

Each page shows a dev-only **arm badge** (top-right) and **A/B/C notes** at the bottom — both
removed before launch. Ships as a **feature-flagged reorder in the Next.js app**, not this
static file (the static files are the review/mockup artifact).

## The combined scholar component

The scholar block stacks all three credibility signals in one card — now with **all-real data**:

1. **Name** (links to profile) — e.g. Dr. Tesneem Alkiek
2. **Title / credential** — "Assistant Director of Research" (real)
3. **Short bio** (expands on click; in the DOM on load so AI reads it) (real)
4. **"Author on this topic:" + their works** — e.g. *Marriage and Gender Roles in Islam* (the sharpest cue on a topic page)
5. *(invisible)* **Person schema** — `jobTitle` + `worksFor` + profile URL — the machine-verifiable layer

**Credential + bio depth is the security-tunable, opt-in layer** — trim it per scholar as the
safety conversation requires. The **authored-works line and structured identity stay
regardless**, so the SEO/GEO signal survives even when the visible bio is lean.

All 6 live scholars have a topic-relevant paper on this hub, so all 6 remain — including Dr.
Jonathan Brown (*Do the Qur'an and Sunnah Speak More Often to Men than Women?*). On hubs where
a scholar has no on-topic work, the topic-relevance rule drops them.

## Measurement (run alongside the test)

- **Human journey** *(the split reads this best)*: click-through into papers, scroll depth, engaged time, bounce / return-to-search.
- **SEO**: rankings on target queries, organic CTR, impressions (Search Console).
- **GEO**: AI citation / mention rate (Profound / Raqib), AI-Overview presence.

**Important:** don't serve crawlers different layouts (cloaking risk / split crawl signals).
Use the live split **only for human-behaviour metrics**; judge SEO/GEO with a **phased** read
(ship the human-winner, measure ranking / citation lift over following weeks) or a
**page-level** test (different topics get different structures, compare).

**Powering:** these are new, low-traffic pages — a three-way split can stay underpowered for
months. Recommendation — **start A vs. B on the highest-traffic topic**, add C in a second
round once answer-first vs. frame-first is settled.

## Open items before launch
- [ ] Confirm opt-in status per scholar for the visible credential/bio layer
- [ ] Add `sameAs` external links (Georgetown, Scholar, etc.) to Person schema where scholars are comfortable — the highest-value machine signal
- [ ] Approved wording for the "not all content is vetted the same way" caveat (still stubbed)
- [ ] Dill UI/UX review → amend template → rebuild via `build_abc_variants.py`
- [ ] Wire real paper/blog/video/profile links (currently `#` stubs)
