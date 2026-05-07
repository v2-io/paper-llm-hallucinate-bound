# RC1 questions for review — paper 3

*Prepared 2026-05-06 alongside `paper-rc1.pdf`. Build state: §1-§6 body at 9pp (NeurIPS budget), full PDF 26pp with appendices A-F + references. One unresolved cite (`lie-sullivan-teckentrup-2017`) renders as `[?]` placeholder pending pipeline fix; anonymization scan clean. Below: open decisions with my recommended answer for each.*

---

## Q1. Abstract — known stale, what to do?

**State.** Abstract lives in `meta.md`. It still references **§7.1** ("positive results showing achievable negligibility exist as a counter-current; §7.1 surveys both directions") — but the current structure has §1-§6 + appendices A-F. There is no §7. The right anchor is `^sec-strand1` in `F-related-work-extended.md` (§F.1).

The abstract was also written before the reshape, and its content reflects an earlier framing in places (e.g., it mentions Track 2's two constants — local √2 and global π/√2 — and the Hellinger 1/√2 companion bound; correct in substance but probably too detailed for an abstract).

**Recommendation.** Two-stage:

- *(now, blocking)* Fix the §7.1 reference. Either change to "Appendix F.1" or drop the parenthetical entirely. I lean toward dropping — the parenthetical is asymmetric (we don't survey the lower-bound side parenthetically either) and the abstract is already long.
- *(later, when body is final)* Take a pass on length. Current abstract runs ~30 lines; NeurIPS norm is ~10–15. Both papers 1 and 2 have the same length issue per my reviews of those — there's a shared opportunity here. Specific candidates to compress: the second-paragraph constants enumeration (the local √2 / global π/√2 / Hellinger 1/√2 detail can move to §4), and the conjugate-Gaussian sentence at the end (which feels appendix-grade for an abstract).

I recommend doing the §7.1 fix today (1 line), and queuing the abstract rewrite for after we settle on §4 length.

---

## Q2. §4 length — currently 3pp vs original 2pp target

**State.** §4 Main Results (Theorem 4.1 Umbrella + Track 1 + Track 2 instantiations + (H2′)/(H4′) hypotheses inline + Theorem 4.4 No-go + Theorem 4.5 Čencov uniqueness + (H_κ) hypothesis + Corollary 4.7 Architectural factorization) currently lands at ~3pp. Original VISION.md target was 2pp. Body total is at 9pp = exact NeurIPS budget; over-budget by 1pp would force overflow into §5 / §6 trim or appendix-shift.

**Recommendation.** **Keep at 3pp.** Body fits the budget, the section earns its length (six numbered statements doing distinct structural work), and trimming would either compress the Remarks (which are pulling weight pedagogically) or remove the parallel Track-1-vs-Track-2 statement structure (which is the paper's spine). The 2pp original was a pre-write estimate; the realized content needs the room. If we hit budget pressure later (e.g., reviewers ask for an experiment, or a missing-citation discussion expands related work), §4 is one of the natural sources of compression — but I wouldn't trim pre-emptively.

Alternative if you disagree: the most compressible section in §4 is §4.1 (the umbrella theorem statement) where the (H2′) / (H4′) hypothesis statements run long inline. Could move the full hypothesis text to §3 and keep §4.1 to one-line invocations. Saves ~0.3pp at the cost of slightly forward-distributed structure.

---

## Q3. Lie-Sullivan-Teckentrup unresolved cite — leave or rephrase?

**State.** F.2 (Strand 2: Bayesian inverse-problems posterior stability) has the sentence "\citet{lie-sullivan-teckentrup-2017} give Hellinger-distance bounds for randomized forward models." The bibkey doesn't have an entry yet. Adding it triggers the hyperref endlink/startlink crash documented in the pipeline inbox — so until that pipeline fix lands, the cite renders as `[?]` placeholder.

**Recommendation.** **Leave as `[?]` placeholder** until the pipeline fix lands. The placeholder is visible to a referee but doesn't break content; rephrasing F.2 to drop the cite would lose a substantively-relevant adjacent strand from the related-work landscape. Once the pipeline owner addresses the underlying super-natbib + cleveref + page-spanning interaction, we add the entry properly. If pipeline fix doesn't land before submission, fallback is to rephrase that one sentence to drop the explicit Lie-Sullivan-Teckentrup cite (the surrounding Strand 2 paragraph still covers Hellinger / randomized-forward-models territory via Sprungk et al. and others).

---

## Q4. Old `src/` directory — archive now or hold?

**State.** `src/` (pre-reshape) and `src/re/` (current canonical) both exist. The build manifest `OUT.re-paper.md` points to `src/re/`. The old `src/` is no longer referenced by any active manifest, but it's still in the repo. Per AGENTS.md §3.4 we don't archive prematurely; the question is whether we've validated `src/re/` as the keeper.

**Recommendation.** **Archive `src/` once you've signed off on RC1.** Concretely: `git mv src _archive/src-pre-reshape/`, then rename `src/re/` → `src/` (so paths in the manifest become `src/01-introduction.md` etc. without the `re/` prefix), and update the manifest. This is a clean break that future agents will understand at a glance. I haven't done it yet because (a) the reshape validation depends on your RC1 review, and (b) the move is hard-to-reverse and warranted explicit confirmation per AGENTS.md "executing actions with care." Recommend doing it after you've reviewed paper-rc1.pdf and we've addressed any structural feedback.

(Same convention paper 2 follows: their `OUT.full-paper-re.md` is the reshaped version; once they validate, presumably they'll do the same archive-and-rename.)

---

## Q5. Anonymization

**State.** Re-checked `pdftotext out/re-paper.pdf` against the deny list (`joseph`, `wecker`, `0009-0004`, `v2-io`, `zenodo`). Clean — no hits.

**Recommendation.** No action; flagging just for confidence.

---

## Q6. Track 2 as headline

**State.** VISION.md committed Track 2 (Fisher-Rao, Čencov uniqueness) as the headline route, with Track 1 (transport-inequality) as parallel. The introduction reads "Universal, dimension-free, no domain-specific parameters... We call this Track 2. A parallel Track 1 derivation... recovers the canonical Stuart-school cascade as a special case... Track 2's universal constant is what makes the composition novel; Track 1 demonstrates that the composition contains the existing Bayesian-inverse-problems lineage as a strict sub-case."

**Recommendation.** **Keep as committed.** The headline-vs-parallel framing reads cleanly in §1 and the parallel structure carries through §3-§5 without strain. The only place I'd watch is the abstract — Track 2's constant enumeration takes up the largest single block of the abstract right now, which is consistent with its headline status, but could be trimmed if we tighten the abstract overall.

---

## Q7. Borrowable ideas from papers 1 and 2

*From reading the other two papers while writing those reviews:*

- **Paper 1's Table 1 in §4.4** (concrete empirical anchor in main body, three-controller drift sweep). Paper 3's Appendix C has the conjugate-Gaussian numerical companion; one summary line lifted into §4 would give referees a concrete instantiation hook. Recommend: a short "Concrete instantiation" paragraph at the end of §4 pointing to Appendix C — half-paragraph, no table needed in main body.
- **Paper 2's §1.2 Scope-and-Limitations placement before §2 Setup** (early off-ramp / definitional precision). Paper 3 has limitations only in §6. Recommend: lift the "we bound a *displacement*, not a *frequency*" framing into §1, since that's the most likely first-pass reader misread.
- **Paper 1's §2 cite-and-distinguish density** is fuller than paper 3's compressed §2 (paper 3 routes detail to §F to save body pages). I think paper 3's compressed §2 is the right tradeoff given page budget — but worth re-reading paper 1's §2 as a model when polishing §F.1 / §F.2.

I haven't applied any of these yet; flagging them for your call.

---

## What I'd do next, given your sign-off

1. *(today, no decision needed)* Drop §7.1 reference from abstract (Q1 stage 1). 1-line edit.
2. *(today, with sign-off on Q4)* Archive `src/` → `_archive/src-pre-reshape/`, rename `src/re/` → `src/`, update manifest. ~10-line diff.
3. *(today, with sign-off on Q7 item 1)* Add Concrete-instantiation paragraph in §4 pointing to Appendix C. ~half-paragraph.
4. *(today, with sign-off on Q7 item 2)* Lift "displacement, not frequency" framing into §1. ~one paragraph addition or rewording.
5. *(deferred until pipeline fix lands)* Add `lie-sullivan-teckentrup-2017` bib entry, verify build clean.
6. *(deferred until body is final)* Abstract rewrite pass (Q1 stage 2).

Or you say "all five today, just do them" and I run with that. Or "not yet, wait for my full review."
