# OUT.neurips-2026-paper.md — 9-page-budget manifest for NeurIPS 2026 main-track submission

*Same `src/` segments as `OUT.full-paper.md`; per AUTHORING §7.2 (reuse-over-re-edit) trim is *manifest-level row-commenting*, not segment-level cuts. If the build reports overage, per-paper agent comments out rows via `<!-- | ... | -->` form rather than editing segments.*

*Per source OUTLINE risk register: page-fit is **comfortable at 9 pages, probably 8.5**. Two-track structure (transport + Fisher-Rao) compresses cleanly. Migration leaves the manifest near-identical to `OUT.full-paper.md` — no rows commented out at migration time. Compression order recorded for the per-paper agent if the build later reports overage:*

1. **§6.1 What the bound says/doesn't doesn't** — could collapse the (i) goal-pairwise dispersion + (ii) (H_neutral)-conditional evidence-only to a footnote-cum-prose-paragraph.
2. **§6.5 Failed routes recorded** — already a summary; could compress to a single paragraph (full statements live in Appendix A).
3. **§5.7 / §5.8** — could collapse the two-tracks-unified-at-distance + universal-constant-buys subsections.
4. **§5.6 Theorem 5.5 (Conjugate-Gaussian Euclidean)** — could move to Appendix C (paper-internal cross-ref already exists).

Appendices are unbudgeted at NeurIPS, so A–D stay regardless. The references section is unbudgeted.

| § | Type     | Slug                                                            | Title                                                       | Stage |
|---|----------|-----------------------------------------------------------------|-------------------------------------------------------------|-------|
| 1 | Section  | [intro](src/01-introduction.md)                                 | Introduction                                                | draft |
| 2 | Section  | [setup](src/02-setup.md)                                        | Setup — belief-goal-coupled architectures + bias quantity   | draft |
| 3 | Section  | [track1-transport](src/03-track1-transport.md)                  | Track 1 — transport-inequality cascade                      | draft |
| 4 | Section  | [no-go](src/04-no-go.md)                                        | No-go on Euclidean chart norms                              | draft |
| 5 | Section  | [track2-fisher-rao](src/05-track2-fisher-rao.md)                | Track 2 — universal Fisher-Rao constant under (PI)+(R)+(K)  | draft |
| 6 | Section  | [discussion](src/06-discussion.md)                              | Discussion                                                  | draft |
| 7 | Section  | [related-work](src/07-related-work.md)                          | Related work                                                | draft |
| 8 | Section  | [limitations](src/08-limitations-conclusion.md)                 | Limitations and conclusion                                  | draft |
| – | Bibliography | [references](src/references.md)                             | References                                                  | draft |
| A | Appendix | [failed-routes](src/A-failed-routes.md)                         | Failed routes                                               | draft |
| B | Appendix | [hypothesis-verification](src/B-hypothesis-verification.md)     | Hypothesis verification details                             | draft |
| C | Appendix | [conjugate-gauss-numerics](src/C-conjugate-gaussian-numerics.md) | Conjugate-Gaussian numerical comparison                    | draft |
| D | Appendix | [parametric-euclidean](src/D-parametric-euclidean-translations.md) | Generalized parametric Euclidean translations            | draft |
