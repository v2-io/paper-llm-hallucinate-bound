# LOG.md — 03-llm-hallucinate-bound history

*Append-only. Reverse-chronological (newest first). Never edit prior entries — LOG is the permanent record. Future agents reading this should be able to reconstruct what was tried, what worked, what failed, and why.*

For active backlog see `TODO.md`. For umbrella-level history see `~/src/neurips/LOG.md`. The source paper's full Pass-1 → Pass-4 audit cycle is the historical record at `~/src/neurips2026/03-hallucinate/LOG.md` and is intentionally **not** re-logged here — this LOG starts fresh from the migration milestone forward.

---

## 2026-05-05 — Migration scaffolding

Migration agent #3 began per `MIGRATE-TODO.md` §A3. Joseph's framing on entry: *"think of it as your paper, I trust your judgment; no idea which paper will make fastest progress, feel free to see any good ideas — all of you have the same training and same instructions and same trust given."* No pre-work orientation file landed in `_archive/` for this paper (paper #1 and #2's first migration agents wrote one before starting; agent #3 carried orientation in conversation rather than committing it to disk after Joseph's "don't worry about drafting it").

**Scaffolding milestone.** Created submodule layout per AUTHORING §7.1: `audits/`, `out/` (build artifacts, gitignored), `spikes/`, `src/`. Skipped `simulations/` and `results/` — B-N8 is theory-only, no empirical anchor (the bound is a conditional theorem under named geometric assumptions; Track 1 cascade has decades of empirical use in Bayesian inverse problems but no original sims belong to this paper). `.gitignore` covers `out/` + `.DS_Store`. `meta.md` carries the post-Pass-2 locked title (*"How Much Can LLMs Hallucinate? An Upper Bound via Coupling and Ambiguity"*) + author block (suppressed in default anonymized builds by the `neurips_2026` sty) + abstract verbatim from `paper-draft.md` lines 5–15. `TODO.md` distills the residual content from source `OUTLINE.md` so the per-paper agent has a clean handoff (smaller surface than papers #1 / #2 — Pass-4 is *audit response complete on substance*, math tighter than Pass-2 entry).

**Migration framing — parity-first** (per Joseph's prior reframe to agent #2). Migration agent's job is parity, not iterative improvement. OUTLINE Pass-N carry-over items go into `TODO.md` for the per-paper agent; mathematical-disambiguation choices stay there. Drive-by mechanical fixes (anonymization, citation-form normalization, heading-prefix strip) *are* migration work and apply during segment authoring, with LOG entries for traceability. The 9pp budget is comfortable per OUTLINE risk register; manifest-level subsetting via `<!-- ... -->` row commenting (AUTHORING §7.2) is the trim path the per-paper agent inherits, not the migration agent's territory.

**Migration-time anonymization scan returned zero hits** across the four-category vocabulary watch (`logogenic`, `directed-separation`, `ASF`, `PROPRIUM`, `AXIOMATA`, `CHRONICA`, `MEMORATA`, `VERA`, ELI names, personal identifiers, ASF Zenodo DOI). Pass-3 / Pass-4 sweeps appear to have caught everything the OUTLINE flagged. Submission-time re-verify is standard hygiene; flagged in `TODO.md` preflight checklist.

**What's next.** Body segments §1–§8 from `paper-draft.md` — 14 inline-bold theorem callouts to convert + 18 `\tag{N}` → `^eq-` anchors + cross-references throughout; citation migration via `bin/migrate-cites` (signed off per `PIPELINE-TODO.md §C1.4`) folds into segment authoring, pilot on §1 before bulk apply. Then appendix segments A–D (per-letter granularity); manifests; build verification; `prior-art/` port; final tracker polish + push.
