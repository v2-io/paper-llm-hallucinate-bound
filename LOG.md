# LOG.md — 03-llm-hallucinate-bound history

*Append-only. Reverse-chronological (newest first). Never edit prior entries — LOG is the permanent record. Future agents reading this should be able to reconstruct what was tried, what worked, what failed, and why.*

For active backlog see `TODO.md`. For umbrella-level history see `~/src/neurips/LOG.md`. The source paper's full Pass-1 → Pass-4 audit cycle is the historical record at `~/src/neurips2026/03-hallucinate/LOG.md` and is intentionally **not** re-logged here — this LOG starts fresh from the migration milestone forward.

---

## 2026-07-29 — Post-review sync: title rot resolved, as-submitted state pinned

Reviews returned 2026-07-23 (submission 33977: ratings 3 / 1 / 2, meta-review negative on novelty-articulation, LLM-connection, and accessibility). No paper content touched here — NeurIPS forbids revisions during the response period, and this pass is bookkeeping so the response can cite the submitted PDF accurately.

**Title rot — three titles existed, and the repo advertised the wrong one.** The chain, all on 2026-05-07:

| | Title | Where it survived |
|---|---|---|
| original (2026-05-05) | *An Upper Bound via Coupling and Ambiguity* | `README.md` H1 + description — **now fixed**; also still the un-synced title in the **OpenReview submission form field** |
| `ab759d6` | *An Information-Geometric Upper Bound on Goal-Coupling Displacement* | nowhere live |
| `280762f` (final) | *An Upper Bound on Goal-Coupling Displacement* | `meta.md`, the submitted PDF |

The last-second edits landed in `meta.md` (hence the PDF) but never propagated to the README or to OpenReview's title field. Reviewers read the PDF, so this cost nothing in review — but the OpenReview field still shows the old title publicly, which is an **author-side fix outside this repo** and is flagged for Joseph, not resolved here. `LOG.md` / `TODO.md` / `audits/` occurrences are historical record and were deliberately left alone; the README now carries an explicit title-history note so no future agent "corrects" the live title backwards.

**Manifest header was stale.** `OUT.llm-hallucinate-neurips-2026.md` still called itself `OUT.re-paper.md`, described the `src/re/` reshape as in-progress, and said the `src/re/` → `src/` rename would happen when it validated. The reshape completed and old `src/` was archived; the rename never happened and `src/re/` is simply the live segment dir. Header now says that plainly rather than describing a plan.

**Dead manifest pointer fixed.** The Bibliography row had pointed at `src/references.md` since migration — a file that never existed. Harmless: `bin/build`'s bibliography branch short-circuits before `render_segment`, emitting `\bibliography{<stem>.references}` and never reading the path, so references always rendered correctly. But a row pointing at nothing invites a future agent to author a manual list there, which is exactly wrong. Created the stub, matching paper 01's existing convention and comment.

**As-submitted state pinned.** Tag `submitted/neurips-2026` at `dd50f7f` (last content commit before submission), plus `submitted-neurips-2026.pdf` — a frozen blind build under a stem no manifest owns, so `bin/build` cannot clobber it. This closes a real gap: the tracked `llm-hallucinate-neurips-2026.pdf` is regenerated on every run and was in fact overwritten twice on 2026-07-29 alone, so it is not a record of anything.

*Basis for calling the current source as-submitted:* git shows no source commits between 2026-05-07 and 2026-07-29 except the 2026-05-22 `meta.md` author-info edit, which only affects `--preprint` / `--final` renders. Cross-checked by word-frequency comparison of a fresh build against the stamped non-anon copy in `~/Documents/submitted-papers/`: every content phrase matches, and vocabulary differences are confined to the author block, the stamp banner, and the preprint footer. Residual caveat, stated rather than hidden: OpenReview records the submission as *modified 27 May 2026*, and whether that was a metadata-only edit or a PDF re-upload cannot be determined from this repo. Since no source commit exists in that window, a re-upload would have come from this same source — but the authoritative artifact is the PDF downloadable from OpenReview, and dropping that in alongside the frozen copy would remove the last bit of inference.

---

## 2026-05-05 — Migration scaffolding

Migration agent #3 began per `MIGRATE-TODO.md` §A3. Joseph's framing on entry: *"think of it as your paper, I trust your judgment; no idea which paper will make fastest progress, feel free to see any good ideas — all of you have the same training and same instructions and same trust given."* No pre-work orientation file landed in `_archive/` for this paper (paper #1 and #2's first migration agents wrote one before starting; agent #3 carried orientation in conversation rather than committing it to disk after Joseph's "don't worry about drafting it").

**Scaffolding milestone.** Created submodule layout per AUTHORING §7.1: `audits/`, `out/` (build artifacts, gitignored), `spikes/`, `src/`. Skipped `simulations/` and `results/` — B-N8 is theory-only, no empirical anchor (the bound is a conditional theorem under named geometric assumptions; Track 1 cascade has decades of empirical use in Bayesian inverse problems but no original sims belong to this paper). `.gitignore` covers `out/` + `.DS_Store`. `meta.md` carries the post-Pass-2 locked title (*"How Much Can LLMs Hallucinate? An Upper Bound via Coupling and Ambiguity"*) + author block (suppressed in default anonymized builds by the `neurips_2026` sty) + abstract verbatim from `paper-draft.md` lines 5–15. `TODO.md` distills the residual content from source `OUTLINE.md` so the per-paper agent has a clean handoff (smaller surface than papers #1 / #2 — Pass-4 is *audit response complete on substance*, math tighter than Pass-2 entry).

**Migration framing — parity-first** (per Joseph's prior reframe to agent #2). Migration agent's job is parity, not iterative improvement. OUTLINE Pass-N carry-over items go into `TODO.md` for the per-paper agent; mathematical-disambiguation choices stay there. Drive-by mechanical fixes (anonymization, citation-form normalization, heading-prefix strip) *are* migration work and apply during segment authoring, with LOG entries for traceability. The 9pp budget is comfortable per OUTLINE risk register; manifest-level subsetting via `<!-- ... -->` row commenting (AUTHORING §7.2) is the trim path the per-paper agent inherits, not the migration agent's territory.

**Migration-time anonymization scan returned zero hits** across the four-category vocabulary watch (`logogenic`, `directed-separation`, `ASF`, `PROPRIUM`, `AXIOMATA`, `CHRONICA`, `MEMORATA`, `VERA`, ELI names, personal identifiers, ASF Zenodo DOI). Pass-3 / Pass-4 sweeps appear to have caught everything the OUTLINE flagged. Submission-time re-verify is standard hygiene; flagged in `TODO.md` preflight checklist.

**What's next.** Body segments §1–§8 from `paper-draft.md` — 14 inline-bold theorem callouts to convert + 18 `\tag{N}` → `^eq-` anchors + cross-references throughout; citation migration via `bin/migrate-cites` (signed off per `PIPELINE-TODO.md §C1.4`) folds into segment authoring, pilot on §1 before bulk apply. Then appendix segments A–D (per-letter granularity); manifests; build verification; `prior-art/` port; final tracker polish + push.

---

## 2026-05-05 — Migration milestone landed

Body §1–§8 + bibliography row + appendices A–D all migrated and committed. Both manifests build clean: `OUT.full-paper.md` → 37pp PDF, `OUT.neurips-2026-paper.md` → trim variant (~similar; per OUTLINE risk register page-fit is comfortable at 9pp main content with no rows commented out at migration time, per AUTHORING §7.2 reuse-over-re-edit). All cross-refs resolve via cleveref; equation anchors use `^eq-` prefix; theorem callouts use `> [!theorem|lemma|corollary|hypothesis]` with display math pulled out below the callout per the kramdown-table-heuristic + display-math-fragments-callout workarounds (the latter is paper #1's pipeline-inbox flag from 2026-05-05).

**Conventions adopted during migration:**

- *Math notation:* `\mid` for conditional `|`, `\Vert` for norm `\|` everywhere in source — kramdown's table heuristic eats paragraphs with bare `|` in inline math when multiple conditional-probability shapes co-occur.
- *Theorem callouts with embedded display math:* statement in callout body using inline-math `$...$` only; full equations pulled out below the callout as anchored `$$ ... $$ ^eq-anchor` with `[[#^eq-anchor]]` reference from inside the callout. Same pattern for proofs containing display math.
- *Cite-keys* canonicalized to `refs/entries/<authors>-<year>-<slug>` form via a mapping pass at the end of authoring: 145 replacements across 13 files. Three notable disambiguations: `kalai-vempala-2023` → `kalai-2023-calibrated`; `kalai-nachum-vempala-zhang-2026` → `kalai-2025-why` (Nature 2026 update with arXiv 2025 noted in entry); `hosseini-hsu-taghvaei-2025` → `hosseini-hsu-taghvaei-2024-conditional-ot`.
- *Optional-arg cite form:* `\cite[Theorem N]{key}` for theorem references (Kallenberg, Polyanskiy-Wu, Stuart, Tsybakov-Lemma-2.4 etc.). Standard natbib syntax; passes through raw-TeX policy.

**Migration-time anonymization sweep returned zero hits** across the four-category vocabulary watch (per AUTHORING §3.5); `bin/refs lint 03-llm-hallucinate-bound` reports 0 anonymization findings, 4 MISSING (the citation-gap items in `TODO.md`), 55 UNVERIFIED (per-paper-agent territory per `TODO.md` preflight checklist).

**Per-paper-agent territory** for downstream work, captured in `TODO.md`: 4 missing-key adds (`lie-sullivan-teckentrup-2017`, `parr-dacosta-friston-2019`, `su-kempe-ullrich-2024`, `wu-grama-szpankowski-2024`); citation verification sweep (`bin/refs verify` for ~55 cites; Pass-3 spike on source returned 0 FAILED so verification likely transfers); reviewer-objection axes (per OUTLINE risk register); compression candidates if build reports overage (§6.1 / §6.5 / §5.7-5.8 collapse / §5.6 → §D move).
