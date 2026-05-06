# VISION.md — 03-llm-hallucinate-bound (B-N8)

*Strategic frame for the reshape from current 27-page body to NeurIPS-form ~8-page main text. Companion to `TODO.md` (live work) and `LOG.md` (history). The structural blueprint we're working against is `~/src/neurips/OUTLINE-STRATEGY.md` at the umbrella, modeled on \citet{jin-yang-wang-jordan-2020}'s "Provably Efficient RL with Linear Function Approximation".*

---

## The frame: Truth → Strength → Wisdom → Beauty

This paper has been worked through Pass-1 → Pass-4 audit cycles plus a Pass-2 strengthen-sweep that delivered four new theorems and one lemma. **Strength is in good shape.** The math is tighter than at Pass-2 entry; the conjugate-Gaussian rederivation lands the right values; the no-go is counterexample-grade; Čencov uniqueness with sharpness is fully proved; the structural Coupled-class lemma for transformer attention is robust without the in-context-learning correspondence. The four-tier risk register (compression / reviewer pushback / empirical-validation absence / citation-hallucination) has been honestly flagged.

**Wisdom got partially compromised.** Each audit pass added corrective theorems and defensive paragraphs — all good Strength work — but the additions never got reabsorbed into a tighter main narrative. They bolted on. By Pass-4 the paper has 14 theorems, six §6 subsections, six §7 strands, all earning their place individually but cumulatively muting the spine. The result is a paper a sympathetic reviewer can fully verify but cannot read in one pass. A skeptical reviewer never gets to the load-bearing argument because the defensive moves crowd it out.

**Beauty has been deferred entirely.** That's the gap this document is addressing.

The reshape is not "trim 27pp to 9pp" — that framing drove much of the prior anxiety and produced bad ordering recommendations (cut compression-candidate sections first, defer the meaty restructure for later). The reshape is *commit to one clean narrative spine, surface only what serves it in main text, treat everything else as substrate that lives in appendix or doesn't appear*. The paper grows up; it doesn't get amputated.

---

## What the exemplar teaches

\citet{jin-yang-wang-jordan-2020} fits ~30 pages of dense linear-algebra-rich argument into an 8-page main body. The discipline that makes this work:

1. **The informal main result lands in the introduction**, in plain English, before the reader has met the notation. Reviewers who don't read past §1 still know what the paper claims.
2. **Preliminaries are strict-minimalist**: every definition that appears in §3 is referenced in either the main theorem statement or the algorithm pseudocode. Definitions used only in proofs go to appendix.
3. **The main result is followed immediately by Remarks** — bulleted, plain-English, "what does this number actually say?" interpretive comments. Without Remarks, formal theorems function as black boxes; with them, the math becomes intuition-restoring.
4. **The Mechanism section narrates the proof strategy** rather than executing it. One or two Key Lemmas are surfaced formally; everything else is deferred with explicit pointer ("the full proof of Lemma 2, requiring a covering argument over the feature space, is Appendix B"). The reader gets a felt sense of the proof without the derivations.
5. **The appendix is unlimited and is where the paper lives for a verification-grade reviewer**. The main text's job is to make the appendix feel necessary; the appendix's job is to be airtight.

The applicability to B-N8 is direct. We have a math-density profile comparable to the exemplar (heavier in some respects). The 18-page main-body excess is *because* we currently do step-by-step algebra in main text and surface every theorem variant equally; the exemplar discipline closes that gap structurally, not by content cuts.

---

## The spine

In one sentence:

> *Goal-coupling-induced displacement of a Bayesian-style model's post-update state admits a universal-constant upper bound — derivable via either transport-inequality machinery or Fisher-Rao geometry — with the operational reading that the bound factors into architectural coupling strength times residual ambiguity for architectures whose goal-update topology fits the Coupled class (which transformer attention does, structurally).*

The three load-bearing claims:

- **Composition.** LLM-hallucination-theory has the right target but doesn't engage architecture geometrically; Bayesian-inverse-problems posterior-stability has the geometric machinery but doesn't apply to belief-goal-coupled inference. The chain rule of relative entropy on the post-update law composes them.
- **Universal constant under (PI)+(R)+(K).** Čencov-uniqueness forces Fisher-Rao + $\sqrt{2}$. The no-go theorem (no chart-independent universal Euclidean constant) is what makes (PI) load-bearing rather than coincidental.
- **Architectural reading.** The Goal/Update Coupling Class partition (Class 1 / Class 2 / Class 3) carries the κ × 𝒜 factorization; Lemma 6.2 derives Class 3 status for transformer attention from connectivity alone.

**Track 2 (Fisher-Rao) is the headline route.** It carries the universal constant — that's the distinguishing contribution. Track 1 (transport) recovers the canonical Stuart-school cascade as a special case and is mentioned in main text as a parallel derivation, but Track 2 is what the paper is *for*.

---

## Structural implications

What this means for the reshape, at the level of decisions:

**Main text (~8pp) stays only what is load-bearing for the spine:**

- §1 Introduction — composition narrative, informal main result, four contributions.
- §2 Related work — Strands 1 and 2 only (one sentence each).
- §3 Setup — Goal/Update Coupling Class partition (table), bias quantity, (PI)+(R)+(K) axioms, **Lemma 6.2 (Coupled-class attention) stated in §3 not §6** since it's structural, not Discussion.
- §4 Main Results — umbrella theorem stated once with both Track 1 and Track 2 instantiations; the no-go theorem paired with it as the negative result that forces (PI); architectural corollary under (H$_\kappa$). **Bulleted Remarks** unpack each: bound-is-size-not-frequency / universal-under-(PI) / κ×𝒜-architectural-reading / transformer-is-Class-3.
- §5 Mechanism — narrative of the two parallel proofs, both grounded in the post-update chain rule; surface Lemma 3.2 (chain rule) and Theorem 5.1 (Čencov uniqueness) formally; defer everything else with explicit pointers.
- §6 Conclusion — half a page.

**Appendix (unlimited):** all four backstop theorems (Track 2 global, Hellinger, Conjugate-Gaussian Euclidean, exponential-family generalization), Lemma D.2 (chord-arc), Hypothesis (S), all proofs, hypothesis verification details (current §B), conjugate-Gaussian numerical comparison (current §C), failed routes (current §A), full positioning across Strands 3–6, the four-theorems-needed defensive framing, the H$_\kappa$ at-architectural-vs-operating-level distinction with parrot witness, the §6.6 HalluGuard / Chlon comparison.

**Cut entirely (or fold into Remarks):** the §6.3 "Why four theorems are needed" defensive section is replaced by the Remarks structure — if the main-text result is clear, no separate defense needed. The §6.5 "Failed routes recorded" is one sentence in §5 Mechanism + full statement in Appendix A. The §6.6 "Relation to existing decompositions" is one sentence in §2 Related Work.

**The two-tier theorem hierarchy now becomes visible:**

- *Spine theorems* (main text): umbrella + Track 1 + Track 2 + no-go + Čencov uniqueness + Lemma 6.2.
- *Companion / generalization / review-defusing theorems* (appendix): Track 2 global, Hellinger, Conjugate-Gaussian Euclidean, exponential-family, chord-arc lemma.

A reader finishing the main text can name the spine theorems. The appendix exists for the verification-grade reviewer.

---

## Open Truth/Strength items still standing

These need attention before or during the reshape — flagging so the structural commitment doesn't lock in a framing that gets undermined by a substantive correction:

- **Truth/Strength items Joseph mentioned** (paraphrased): we need to fix some Truth/Strength things alongside the Wisdom/Beauty work. I don't have the specific list yet — to be enumerated in the next discussion.
- **The four missing bibkeys** (lie-sullivan-teckentrup-2017 / parr-dacosta-friston-2019 / su-kempe-ullrich-2024 / wu-grama-szpankowski-2024) need adding via `bin/refs add` before the reshape commits to a related-work framing that depends on them.
- **The empirical $\hat\kappa_{\text{processing}}$ estimator** (currently a brief mention in §2.3) — decide whether it stays brief in main text, moves to appendix, or gets formalized further. Affects the operational-reading framing.
- **The (H$_\kappa$) at-architectural-vs-operating-level distinction** — currently a §6.4 defensive subsection. Under the reshape it goes to appendix. Verify that's the right call before committing.

---

## Standing principles for the reshape

- *Truth above all else.* No overclaiming. Mark uncertainty explicitly. The paper's posture is the math's posture.
- *Strengthen before softening.* If a claim looks overclaimed during the reshape, attempt to strengthen first. We have a track record on this paper of strengthening attempts paying off (Pass-2 spike: 4 theorems + 1 lemma; Pass-4 H6 spike: Theorem 5.4-glob).
- *Defensive moves to appendix or out.* Confidence in the spine reads better than defense of every variant.
- *Remarks unpack theorems; main text doesn't algebra-grind.* The Jin et al. discipline.
- *Single clean story over comprehensive coverage.* Comprehensive coverage is what the appendix is for.
- *Time pressure / context pressure are false constraints in this work.* They produce ordering recommendations exactly inverted from what's actually valuable. The right move always honors the substance, even when it costs a session boundary.

---

## Path forward

**`src/re/` clean rework, not in-place refactor of existing `src/`.** The structural changes are substantial enough that in-place editing risks tearing cross-refs faster than we can re-stitch them. Keeping `src/` pristine means we can compare side-by-side and revert cleanly if a structural choice doesn't work. Existing `src/` becomes substrate the way `paper-draft.md` was during migration — read, but not output. New manifest `OUT.re-paper.md` references `src/re/`. When the reshape validates, archive old `src/` and rename `src/re/` → `src/`. Slight disk overhead; substantial coordination risk reduction.

The refactored segments will themselves be authored against the spine and the §-level blueprint above, with each segment carrying just what serves the main-text section it's part of. Theorem-numbering will reset cleanly; the numbering churn we accumulated across Pass-1–Pass-4 is part of what's making the current state hard to read.

The order I'd propose for the reshape itself:

1. Sketch new `src/re/` segment structure as empty stubs + headings, validate the §-level layout against the blueprint without committing prose.
2. Author §1 Introduction first (spine plus informal main result + four contributions). The intro is the spine concentrated; if it doesn't read cleanly, the rest of the reshape is built on a wobbly foundation.
3. Author §3 Setup + §4 Main Results (with Remarks). The math density lands here.
4. Author §5 Mechanism (proof-strategy narrative).
5. Author §6 Conclusion.
6. Author appendices (mostly port + tighten existing src/ segments).
7. New manifest `OUT.re-paper.md` referencing src/re/. Build, visual-confirm.
8. Once validated: archive old src/ → src/_pre-reshape/ (or _archive/), rename src/re/ → src/, update both manifests.

That's the shape. Open to course-corrections at any step.

---

*This document captures the strategic frame as of 2026-05-06. Updated as the reshape progresses; superseded when the reshape lands.*
