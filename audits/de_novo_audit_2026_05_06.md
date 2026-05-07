# De Novo Audit: How Much Can LLMs Hallucinate?

**Date:** 2026-05-06
**Auditor:** Gemini CLI

## 1. Space Reduction & Restructuring (Addressing the >9pp limit)
- **Condense Section 5 (Mechanism):** Section 5 provides derivation sketches for Track 1, Track 2, and the No-go theorem. Since the full derivations are completely written out in Appendix E, Section 5 can be condensed significantly. Integrating the core intuition (the chain rule on the post-update law) directly after Theorem 4.1 in Section 4 and removing the rest of Section 5 would save around half a page.
- **Failed Routes (Appendix A):** The documentation of failed routes (Cramér-Rao, Rate-distortion) is a great example of epistemic discipline. Keep these strictly in the appendix to conserve space; ensure no main-text space is inadvertently spent defending against these unless reviewer feedback demands it.

## 2. Claim Strengthening & Technical Focus
Following the project's "strengthen before softening" mandate:
- **Tighten the Metric Uniqueness Argument:** The No-go theorem on Euclidean chart norms (Theorem 4.4) and the Čencov uniqueness theorem (Theorem 4.5) form a brilliant sequence. Consider explicitly framing Theorem 4.5 not just as "Fisher-Rao is unique," but as "Fisher-Rao is the *only* surviving metric that avoids the Euclidean scale-family pathology while matching KL at second order." This makes the choice of metric feel inevitable rather than merely axiomatic.
- **Generalize the Coupled-Class Claim:** Lemma 3.5 (Coupled-class attention connectivity) is stated as being robust to FlashAttention, causal masking, etc. Determine if state-space models (like Mamba) or linear attention variants also inherently fall into Class 3 due to their recurrent hidden state dependence on the goal. Extending the structural claim from "transformer attention" to broader "autoregressive sequence models with goal-dependent hidden states" would widen the bound's applicability without diluting the claim.