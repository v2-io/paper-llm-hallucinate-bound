# response-prep — NeurIPS 2026 author response (submission 33977)

Raw material for the response, not the response itself. Ratings 3 / 1 / 2 (confidences 2 / 2 / 4).

> **Tracked in a public repo.** Paraphrase reviewer substance; no reviewer pseudonyms, no verbatim review text. Reviews at `~/src/neurips/reviews/neurips-2026/03-llm-hallucinate-bound/` (gitignored, confidential through Aug 10). Rationale in the umbrella `.gitignore`.

The meta-review is negative on theoretical-novelty articulation, LLM relevance, and accessibility — but closes by naming what would substantially strengthen the work, which is more engagement than a dismissal. The lowest rating is at confidence 2 with an explicit admission of not following the arguments, so the AC may discount the score; **the diagnosis should not be discounted**, since it is the same clarity finding all three papers received.

## Constraints

- No paper or supplementary revisions. Cite pages from `../submitted-neurips-2026.pdf` (frozen; the regenerable `llm-hallucinate-neurips-2026.pdf` is not a stable reference).
- 10,000 characters per review; plain text + markdown; no links, no uploads, no anonymity breaks.
- Author-visible window closes **2026-08-03** — confirm against OpenReview's deadline field, since the notification email contradicts itself.

## Two things to get right

- **`J-01` is a correct catch and must be conceded without hedging.** The bound is vacuous once transferred information exceeds ~2.5 nats, and the abstract advertises exactly that regime. Getting this wrong in the response destroys credibility on everything else. Attempt the affinity-coordinate strengthening first (`math/J-01-vacuity-ceiling.md`), then concede cleanly if it doesn't land.
- **`J-02` ("what's new beyond composing known inequalities?") is the decision-relevant one.** Lead with the no-go — that no universal constant exists absent a parameterization-invariance commitment is a negative result, not a composition. Do not defend the `√I` conversion as novel; it isn't, and defending it loses.

## Layout

| Path | What goes here |
|---|---|
| `ISSUES.md` | Per-issue tracker — the working surface. |
| `math/` | Derivations needed before we can answer honestly. |
| `segments/` | Revision drafts. Not usable this period. |
