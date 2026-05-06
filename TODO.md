# 03-llm-hallucinate-bound — TODO

*Live work for B-N8 migration. Recipe in AUTHORING §8. Free to branch into `TODO-citations.md` / `TODO-trim.md` / etc. as scope grows; no fixed schema. For history see `LOG.md`. For umbrella-level migration backlog see `~/src/neurips/MIGRATE-TODO.md`.*

---

## Inbox — flagged 2026-05-06 by build-pipeline agent

**Page-budget reality check — substantial overrun.** `bin/build 03-llm-hallucinate-bound neurips-2026-paper` currently produces a 38-page PDF; main text (§1–§8) ends at page 27, References starts at page 28, Appendix A at page 31. That's **~18 pages over** the 9-page main-text limit. The earlier OUTLINE risk-register note ("comfortable at 9 pages, probably 8.5") doesn't match the current build — please verify directly via `pdfinfo out/neurips-2026-paper.pdf` plus a grep for the References transition, then plan substantial main-text trim and/or aggressive appendix relocation. The current manifest doesn't have any rows commented out. (Page-budget tool `bin/page-budget` is a known PIPELINE-TODO §E3 port-pending item; in the meantime `pdfinfo` + grep-for-section-transitions is the manual check.)

**`[!table] cols="..."` opt-in just landed (umbrella commit `d4218a8`).** `src/02-setup.md:29-43` currently uses a raw `{::nomarkdown}\begin{table}...\begin{tabularx}{\textwidth}{@{}l X X X@{}}...{:/nomarkdown}` block for the Goal/Update Coupling Class partition table — the migration agent's escape hatch when default `tabular` was overflowing. With the new attribute, this can refactor to:

```
> [!table] Goal/Update Coupling Class — partition of architectures by conditional-independence structure. ^tab-class-partition cols="l X X X"
>
> | Class | Goal/update coupling | Topology | Examples |
> |:------|:--------------------|:---------|:---------|
> | Class 1 (Separated) | ... | ... | ... |
> | Class 2 (Partial)   | ... | ... | ... |
> | Class 3 (Coupled)   | ... | ... | Transformer LLM (attention processes goals and observations together — [[#^thm-attention-coupled]]) |
```

This re-enables `[[#^anchor]]` cross-refs (the manual `\Cref{thm-attention-coupled}` at line 40 inside the raw block can become `[[#^thm-attention-coupled]]`) and shrinks the source. AUTHORING §1.4 documents the convention. Optional refactor — the current raw-TeX form renders correctly.

**Bold-prefix vs callout form — verify intentional.** `src/B-hypothesis-verification.md:15` uses `**Hypothesis (S) — own proof of strong log-concavity for Bayesian post-updates.**` as a paragraph-prefix. AUTHORING §1.1 prefers Obsidian `> [!hypothesis] (S) — ... ^hyp-S` callout for theorem-shaped envs; AUTHORING §1.9 allows bold-prefix for plain paragraph headings. The "(S)" naming convention suggests a deliberately-unnumbered named hypothesis, which is fine — but if you want `\Cref{hyp-S}` cross-references to it, it should be a callout. Your call.

**List-renumber across `$$` — fixable at source via 3-space indent.** Confirmed reproduces at §6.4 (`src/06-discussion.md` lines 93–101) and §B.3 (`src/B-hypothesis-verification.md` Conditions 1+2). Each `1. item ... <blank> $$math$$ <blank> 2. item` pattern emits two separate `\begin{enumerate}` envs in the rendered TeX, each starting at item 1. Fix: indent the un-indented `$$...$$` blocks 3 spaces under the preceding list item — kramdown then reads them as continuation content of that item, and the `1./2./3.` items render as a single enumerate with correct numbering. Concrete edit for §6.4:

```
1. *Goal-blind effective kernel.* ...long item text...

   $$I(G; M_{\tau^+}| e_\tau, M_{\tau^-}) \le ...$$ ^eq-goal-blind-kernel

2. *Bounded direct architectural channel.* ...long item text...

   $$I(G; M_{\tau^+}, \Omega_\tau | e_\tau, M_{\tau^-}) = ...$$ ^eq-mi-chain-rule

   $$I(G; M_{\tau^+}| e_\tau, M_{\tau^-}) \le ...$$ ^eq-direct-channel-bound
```

(Three spaces, not a tab; the second item-2 equation also gets 3 spaces because it's also continuation of item 2's body.) AUTHORING §1.6 now documents this convention. Same pattern applies at §B.3. No pipeline change needed.

**`𝒜` (U+1D49C MATHEMATICAL SCRIPT CAPITAL A) used outside math mode — renders as missing-glyph box.** AUTHORING §2.8 (just landed) covers the rule: TeX Gyre Termes lacks math-script-letter glyphs, so calligraphic A in prose needs `$...$` wrapping. The build's compile log shows multiple "Missing character: There is no 𝒜 (U+1D49C) in font" warnings. Same shape across all 7 sites — `κ × 𝒜 factorization` should become `$\kappa \times \mathcal{A}$ factorization`:

- `src/01-introduction.md:17` — `κ × 𝒜 factorization`
- `src/05-track2-fisher-rao.md:67` — same
- `src/06-discussion.md:87, 115, 117` — same shape, three sites
- `src/08-limitations-conclusion.md:23` — same
- `src/B-hypothesis-verification.md:60` — same

The bare-`κ` (U+03BA, Greek small letter kappa) in those phrases renders fine — Greek letters are in TeX Gyre Termes. Only the script-A needs wrapping. Search-and-replace pattern: `κ × 𝒜 ` → `$\kappa \times \mathcal{A}$ ` should sweep all sites cleanly. Verifies via `grep "Missing character" out/full-paper.log` after rebuild.

**Smart-quote vs `$` — not actually broken in PDF.** Your post-revert verification reported smart-quote conversion failing in §C numerical-comparison appendix. Hex-dump of pdftotext output for the σpost√2I phrase shows `e2 80 9c` and `e2 80 9d` — UTF-8 encodings of U+201C / U+201D (proper curly quotes). The intermediate `out/full-paper.tex` has `` ``$\sigma\sqrt{2I}$'' `` ligature form that lualatex renders to typographic curly quotes. Likely explanation: the PDF viewer or pdftotext setting in your local view is rendering UTF-8 curly quotes as straight glyphs. The actual rendered output is correct. Keep the post-revert ASCII `"` form. If you can confirm via a different viewer or hex-dump on your end and the curly bytes are missing, please update with the new evidence.

---

## Migration milestone — landed 2026-05-05 (agent #3)

All scaffolding + body + appendices + manifests + citation canonicalization landed:

- [x] Scaffolding milestone (dirs + `.gitignore` + `meta.md` + `LOG.md` + this file).
- [x] Body segments §1–§8 from `paper-draft.md` → `src/01-introduction.md` ... `src/08-limitations-conclusion.md`. One segment per top-level section.
- [x] Appendix segments A–D → `src/A-failed-routes.md` + `src/B-hypothesis-verification.md` + `src/C-conjugate-gaussian-numerics.md` + `src/D-parametric-euclidean-translations.md`. Per-letter granularity.
- [x] Manifests: `OUT.full-paper.md` (everything) + `OUT.neurips-2026-paper.md` (9pp budget). Both build clean; per OUTLINE risk register page-fit is comfortable at 9 pages, no rows commented out at migration time.
- [x] Citation conversion done at authoring time (`[Author Year]` → `\cite{key}` directly). Cite-key canonicalization via `/tmp/cite-canonicalize.rb` mapping speculative keys to `refs/entries/` canonical form: 145 replacements across 13 segment files; `bin/refs emit 03-llm-hallucinate-bound` writes `refs.bib` (472 lines, ~55 keys). 4 keys still missing from `refs/entries/` — see "Citation migration" section below.
- [x] Build verification: `bin/build 03-llm-hallucinate-bound full-paper` + `bin/build 03-llm-hallucinate-bound neurips-2026-paper` both clean. Visual PDF confirm: title renders correctly, body italics + em-dashes + special chars (Čencov, Iñigo, σ) typeset clean, display equations + theorem callouts + cross-refs resolve, anonymized author block, four `[?]` superscripts visible for the missing-keys flagged below.
- [x] `prior-art/` port from old workspace (`query.md`, `report.md`, `positioning.md`).
- [x] Final commit + push to `v2-io/paper-llm-hallucinate-bound`.

---

## Carry-over from source OUTLINE.md — for per-paper agent post-migration

Source paper is at Pass-4 *audit response complete on substance* (per OUTLINE Live work items). Math is mathematically tighter than at Pass-2 entry — 1 new theorem + 1 new lemma + 1 sharpness clause + 2 architectural-certificate distinctions across Pass-4. Residual surface is smaller than papers #1 / #2 had at their migration time.

### (a) Submission housekeeping

- [ ] **Anonymization grep pass at submission time.** Build-side scanner via `refs/deny-list.yml` runs as part of `bin/build`; manual scan against the four AUTHORING §3.5 categories before commit. Migration-time scan returned zero hits across the four-category vocabulary watch (`logogenic`, `directed-separation`, `ASF`, `PROPRIUM`, `AXIOMATA`, `CHRONICA`, `MEMORATA`, `VERA`, ELI names, personal identifiers, ASF Zenodo DOI). Pass-3 / Pass-4 sweeps appear to have caught everything. Re-verify before the actual submission.
- [ ] **No ASF self-citation.** Zenodo DOI `10.5281/zenodo.19986312` must not appear; spot-check during integration showed clean per source OUTLINE.md, formal verification at `bin/refs lint` time.
- [ ] **Acknowledgments removed at submission.** `> [!ack]` callout (AUTHORING §1.3) auto-suppressed in anonymized builds — leave content for camera-ready.
- [ ] **AI-use disclosure.** Theory-only paper; no methodological-disclosure section needed (handbook §"Author Use of Agents and LLMs" exempts editing/exposition aid).
- [ ] **Contemporaneous-work cutoff (March 1, 2026).** Anxin Guo-Jingwei Li 2026, Zeng et al.\ 2026 HalluGuard, Kalai-Nachum-Vempala-Zhang 2026 (Nature year-of-record) cited in §7 with cite-and-distinguish posture. Pre-March papers get full positioning treatment.
- [ ] **Cross-paper differentiation hygiene.** B-N8 owns κ × 𝒜 factorization / Class 1/2/3 / Fisher-Rao + Čencov universal-constant / no-go-on-Euclidean-charts. B-N4 owns LMI / Lyapunov-survival drive; B-CS1 owns BH-identity / 2×2 / strategic tempo / closed-loop access. (Confirmed in old workspace `common/cross-paper-differentiation.md`.)

### (b) Citation items remaining

- [ ] **Wu-Grama-Szpankowski venue (M5).** Currently cited as 2024 (arXiv year); accepted at ICLR 2025. Either defensible; flag for finalization sweep.

(Per OUTLINE.md Pass-3/4 audit closure: Chlon v1 pin resolved; Kalai-Nachum-Vempala-Zhang Nature 2026 update applied. Remaining surface is the Wu-Grama-Szpankowski venue choice.)

### (c) Trim sweep (deferred until needed)

- [ ] **Main-text trim only if build reports overage.** OUTLINE risk register: page-fit *comfortable at 9 pages, probably 8.5*. Compression order if forced: §6.1 / §6.5 first; §5.7 / §5.8 collapse; §5.6 Theorem 5.5 → §D as last resort. Appendices unlimited. Per AUTHORING §7.2: handle via manifest-level row-commenting in `OUT.neurips-2026-paper.md`, not segment-level cuts.

### (d) Reviewer-objection axes (per OUTLINE risk register)

Per-paper-agent territory. Migration preserves verbatim — defensive paragraphs deadline-permitting.

- [ ] *"Isn't this just Kalai-Vempala or Kalai-Nachum-Vempala-Zhang restated?"* — addressed in §1 + §7.1 via the architecture-engagement (κ_processing) and the geometric-assumption regime (LSI, Lipschitz-posterior, Čencov). Tighten if reviewer still confuses size-vs-frequency axes.
- [ ] *"Isn't this just Stuart 2010 applied to LLMs?"* — addressed via κ × 𝒜 factorization, Goal/Update Coupling Class partition, no-go.
- [ ] *"Doesn't Owhadi-Scovel-Sullivan brittleness contradict your Track 1 stability?"* — addressed by explicit (H1) + (H2$'$) excluding their brittleness regime. §7.4 Strand 4 ("handle carefully") covers the cite-and-distinguish.
- [ ] *"Why Track 2 if Track 1 already works?"* — addressed by dimension-free $\sqrt{2}$ universal constant + small-$I$ tightness Track 1 cannot produce.
- [ ] *"Hosseini-Hsu-Taghvaei already did conditional optimal transport — what's new?"* — addressed by application to belief-goal-coupled architectures with explicit κ-factor + the no-go showing geometric commitment is load-bearing.

### (e) Decision-log carry-overs (per OUTLINE)

For agent context, not action items:

- Two-track structure (transport + Fisher-Rao) is load-bearing: (PI) no-go in §4 makes Track 2's universal $\sqrt{2}$ *necessary*, not just elegant.
- Empirical estimator $\hat\kappa_{\text{processing}}$ via two-goal probing: brief mention in §2.3 only; formal estimator deferred to future work.
- Theorem 5.1 in §5.2; Theorem 5.5 stays in §5.6 main text (not §D).
- Pass-4 corrected $\kappa^{\text{realized}} = 1$ + $C_{T_2} = 2L_{\text{post}}^2\sigma^2$ + Theorem 5.5 prefactor $L_{\text{post}}\sigma$ — conjugate-Gaussian Class 1 example saturates DPI exactly because the data channel is invertible.

---

## Preflight checklist (before any submission build)

- [ ] **Anonymization grep.** Build-side via `refs/deny-list.yml`; four-category manual scan.
- [ ] **Citation verification.** `bin/refs verify` for every `\cite{key}` in segments. Pass-3 spike returned 0 FAILED on the 30+ source citations; verification status should carry forward through bib-emit (PIPELINE-TODO §F5).
- [ ] **No ASF self-citation.** Zenodo DOI `10.5281/zenodo.19986312` absent.
- [ ] **Acknowledgments auto-suppressed.** `> [!ack]` content present for camera-ready, suppressed by build at submission.
- [ ] **AI-use disclosure.** N/A for theory-only / editing-aid usage per handbook.
- [ ] **Contemporaneous-work cutoff (March 1, 2026).** §7.5 / §7.6 carry the cite-and-distinguish.
- [ ] **Cross-paper differentiation hygiene.** B-N8's contributions don't reduce to B-N4 or B-CS1.

---

## Citation migration — pending and ambiguous matches

Cite-key canonicalization done at migration time: 145 replacements across 13 segment files, mapping speculative `\cite{<author>-<year>}` keys to the canonical `<authors>-<year>-<slug>` form used in `refs/entries/`. `bin/refs emit 03-llm-hallucinate-bound` now generates `refs.bib` with 472 lines covering ~55 cited keys.

**4 keys still missing from `refs/entries/`** — flagged for the per-paper agent to add via `bin/refs add`:

- `lie-sullivan-teckentrup-2017` — Lie, Sullivan, Teckentrup, *Hellinger-distance bounds for randomized forward models* (cited in §7.2). Old workspace bib may have this; verify before adding.
- `parr-dacosta-friston-2019` — Parr, Da Costa, Friston, on Markov-blanket apparatus / generalised free energy (cited in §7.6). May be one of the existing `parr-2017-uncertainty` / `parr-2018-generalised` / `parr-2022-active` entries; verify before adding.
- `su-kempe-ullrich-2024` — Su, Kempe, Ullrich, *jailbreaking from a statistical perspective* (cited in §7.5).
- `wu-grama-szpankowski-2024` — Wu, Grama, Szpankowski, *VC-dimension impossibility* (cited in §1, §7.1, §8). Per OUTLINE Pass-4: arXiv 2024 with ICLR 2025 venue accepted; flag whether to use 2024 or 2025 year-of-record.

The build's anonymization scanner will continue to flag these as `[?]` superscripts in the PDF until the entries land.

**Cite-disambiguations that landed during canonicalization** (for future-agent context):

- `kalai-vempala-2023` (my speculative key) → `kalai-2023-calibrated` (Calibrated Language Models Must Hallucinate, STOC 2023). Note: also exists as `kalai-vempala-2024-must-hallucinate` (same paper, 2024 venue update); the per-paper agent may want to consolidate.
- `kalai-nachum-vempala-zhang-2026` → `kalai-2025-why` (renamed in entry to "Evaluating large language models for accuracy incentivizes hallucinations", Nature 2026 with arXiv 2025 noted in `note` field per Pass-4 OUTLINE update).
- `hosseini-hsu-taghvaei-2025` → `hosseini-hsu-taghvaei-2024-conditional-ot`. The 2024 vs 2025 year question may want re-checking against the SIAM/ASA J. UQ 13(1):304–338 publication record; per-paper agent territory.

---

## Risk register (carried from source OUTLINE.md)

- **Compression risk: low.** 9 pages with margin (probably 8.5); the two-track symmetry compresses cleanly.
- **Reviewer pushback risk: medium.** Sophisticated reviewer paths covered above (item (d)). BH-style "hasn't this been done?" frame is the highest-likelihood path.
- **Empirical-validation absence risk: medium-high.** NeurIPS reviewers expect empirical validation; pure theory paper is a known weak spot. Mitigations: (a) the bound is a conditional theorem under standard regularity (LSI verifiable; Lipschitz-posterior is Stuart 2010 standard); (b) Track 2 is mathematically airtight under (PI); (c) the no-go is counterexample-grade. Empirical estimator for $\hat\kappa_{\text{processing}}$ via two-goal probing kept as brief §2.3 mention; formal operationalization is genuine future work.
- **Citation-hallucination risk: low.** Pass-3 citation-verification spike returned 0 FAILED. Foundational citations all verified; recent 2024–2026 papers all in Undermind report's evidence register; year-of-record corrections applied Pass-3 (Sprungk, Latz, Dolera-Mainini, Dolera-Favaro-Mainini); Kalai-Nachum-Vempala-Zhang updated to Nature 2026 source-of-record at Pass-4 with arXiv 2025 noted; Chlon pinned to v1 explicitly.
- **Vocabulary-anonymization risk: low.** Migration-time scan returned zero hits on the four-category watch. Pass-3 / Pass-4 sweeps caught the named risks (`logogenic`, `directed-separation`). Re-verify at submission time as standard hygiene.
