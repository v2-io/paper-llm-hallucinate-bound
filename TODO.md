# 03-llm-hallucinate-bound — TODO

*Live work for B-N8 migration. Recipe in AUTHORING §8. Free to branch into `TODO-citations.md` / `TODO-trim.md` / etc. as scope grows; no fixed schema. For history see `LOG.md`. For umbrella-level migration backlog see `~/src/neurips/MIGRATE-TODO.md`.*

---

## Opus de-novo audit triage — 2026-05-07 (claude-opus-4-7, 1M context)

Audit at `audits/audit-2026-05-06-claude-opus47.md` (382 lines: 8 M-tier + 8 A-tier + 8 S-tier + 10 C-tier + 10 N-tier). The auditor verified all load-bearing math (chain rule, chord-arc, Čencov reduction, no-go, Hellinger, conjugate-Gaussian) and found the math sound. Most findings are tightening; two flagged for priority by the auditor: M1/A1 (the $\sqrt 2$/(H4$'$) headline framing) and S2 ("Track 5.5" naming inconsistency).

**Already answered by prior spikes — no new action.** Three findings (M7, A5, C4) ask about Track 1's recovery of the Stuart-school cascade constant. The A7 spike (`spikes/A7-stuart-school-mapping/report.md`, commit `6b94a72`) already established Theorem A7.1' which generalizes the Stuart-school cascade across the full Strand 2 hypothesis space — strictly stronger than what M7/A5/C4 ask for. When the A7-i through A7-iv integration items land, M7/A5/C4 are resolved.

### O1. (H4$'$) vs $\pi/\sqrt 2$ — spike-worthy strengthening *(M1/A1, auditor's #1 priority)*

**The question.** Theorem 1's Track 2 row says $C = \sqrt 2$ "universal, dimension-free, no domain-specific parameters." This holds *under (H4$'$) uniform-locality* — `ess sup_g KL(P_M+|G=g || P_M+) ≤ δ_⋆` for some $δ_⋆ ∈ (0,1)$. The auditor's structural concern: (H4$'$) is likely *false* in the LLM application's operating regime (Class 3 Coupled with adversarial / rare goals → at least one $g$ with large $\mathrm{KL}_g$ violates the ess-sup uniformly). So $\sqrt 2$ is not the LLM-operating constant; the global $\pi/\sqrt 2$ backstop is. The current paper presents the global as a "fallback" — but for the headline application it's the actual bound.

**Why this is spike-worthy** (per AGENTS §3.1 escalation paragraph): the auditor's recommendation — *"rebrand as 'two universal Fisher-Rao constants — locally-tight $\sqrt 2$ in the uniform-local regime, globally-valid $\pi/\sqrt 2$ throughout — both forced by Čencov'"* — is a presentation strengthening (move global into the headline). But there's a *deeper* strengthening hidden behind that move:

- *(direction A)* Can we find a hypothesis weaker than (H4$'$) that still yields $\sqrt 2$ — particularly one that holds *structurally* in the LLM application (e.g., bounded attention temperature, bounded softmax-cap, bounded-likelihood-ratio architecture conditions) rather than as a regime-condition on the goal-conditional KL?
- *(direction B)* Can we close part of the $\sqrt 2$-vs-$\pi/\sqrt 2$ gap globally — i.e., a bound $\mathbb E[d_{FR}^2] \le C(I_M)\,I_M$ where $C$ smoothly interpolates between 2 (small $I_M$) and $\pi^2/2$ (antipode), strictly tighter than the flat $\pi^2/2$? My back-of-envelope: chord-arc gives the closed form $d_{FR}^2 = 16\arcsin^2(\mathrm{Hel}/\sqrt 2)$ on the unit $L^2$-sphere. Tsybakov 2.4 is loose by factor 2 at small KL (locally $\mathrm{Hel}^2 \approx \mathrm{KL}/4$, while Tsybakov's $\mathrm{Hel}^2 \le \mathrm{KL}/2$). A sharper Hel-KL inequality + the closed-form chord-arc might compose into a tight interpolant.
- *(direction C)* Boundary case — find the fundamental reason $\pi/\sqrt 2$ is genuinely the best globally-valid constant under (PI) alone, and document it.

All three are legitimate spike outcomes. The trichotomy from §5.4 applies: succeed-beyond (a strictly-tighter global constant), succeed-at-claim (recover $\sqrt 2$ under structural-LLM hypothesis), succeed-at-finding-the-boundary (why $\pi/\sqrt 2$ is sharp).

**Recommended action.** Launch an Opus spike on this (analogous to A7's). Output to `spikes/O1-tighter-track2-constants/report.md`. Worth the depth — the result lands directly in the paper's headline rate statement. I'm queuing rather than triage-resolving per the new §3.1 discipline.

### O2. Bias-quantity notation $\|P, Q\|_{\mathcal M}$ → $d_{\mathcal M}(P, Q)$ *(M2)*

**Knock-out.** `src/re/03-setup.md:9`'s `||P_M+|G, P_M+||_M` reads as a norm-of-two-distributions-separated-by-comma, which isn't standard. The body text already uses $W_2(P,Q)$ and $d_{FR}(P,Q)$ which compose with $d_{\mathcal M}(P,Q)$ cleanly. Replace the bias-quantity definition + propagate. ~5 occurrences, mechanical.

### O3. "Track 5.5" / "Track 3 Hellinger" — non-monotone numbering *(S2, auditor's #2 priority)*

**Knock-out.** `src/re/C-conjugate-gaussian-numerics.md:21,33` references "Track 5.5 Euclidean" with no Track 3, 4, or 5 defined. Likely leftover from earlier draft. Auditor's renaming proposal: keep Track 1 (Talagrand) + the Track 2 family (Track 2-FR locally-tight, Track 2-FRG global, Track 2-Hel Hellinger, Track 2-Eucl Euclidean translation). Or simpler: drop the Track-N numbering for the Euclidean translation entirely, just call it "Euclidean translation of Track 2" and refer by anchor. Either fine; latter is less typing.

### O4. Lemma 3.5 caveat-placement + magnitude-vs-reachability sentence *(M8/A2/S8 — converges with my prior A4)*

**Knock-out, folds with A4.** Three findings (M8 final paragraph, A2's "non-degenerate qualifier is quiet," S8's caveat-placement) all converge on: the structural/reachability-vs-magnitude distinction in Lemma 3.5 is in the body but quiet; reader of intro skims past it. Auditor's suggestion: one explicit sentence in the intro / table area that "structural classification is at the architectural level (what attention *can* do); the *quantitative* coupling magnitude $\kappa_{\text{processing}}$ requires additional assumptions." This folds cleanly with my prior A4 (prose-to-formal scope tightening for Lemma 3.5). One small edit at intro + one at the table; carry the magnitude-vs-reachability sentence too.

### O5. Conjugate-Gaussian setup ambiguity around $\Omega|G$ *(M6)*

**Knock-out.** `src/re/C-conjugate-gaussian-numerics.md:3` has two readings of $\Omega|G$ — (a) directly goal-conditional ignoring $\theta$, or (b) marginalizing over $\theta$. The math uses (a); a one-line clarification in the setup ("we treat $\Omega|G$ as goal-determined directly; the world-state $\theta$ enters only via the agent's prior, not the observation") removes the ambiguity. Pairs naturally with A7-v's notation clarification on $\rho_{\text{LSI}}$ in the same segment.

### O6. Future-directions paragraph in conclusion is dense *(S7)*

**Modest.** Single 6-sentence paragraph at `src/re/06-conclusion.md:9` lists five distinct future directions. Auditor: "either bullet them or pick the highest-leverage two and expand." Pairs naturally with the existing Codex H6 fix (move "empirically accessible κ" sentence into a more developed future-directions slot). Recommend: bullet the five, expand the two highest-leverage ($\kappa$-empirical-instantiation + extension-to-non-(H4$'$)-regime), trim the rest.

### O7. KL-to-Fisher-Rao remainder $R_3(δ_⋆)$ — verify the $\mathbf I_{\min}^{-3/2}$ scaling *(M4)*

**Modest spike-or-knock-out.** `src/re/E-proofs.md:39` gives $R_3(δ_⋆) = (\mathcal T_⋆/3)\sqrt{2δ_⋆/\mathbf I_{\min}^3}$. Auditor verified the structure but flagged: the cube of the geodesic norm $\|\delta\|^3$ converts to coordinate-norm with a $\mathbf I_{\min}^{-3/2}$ factor, plausibly correct but worth one explicit derivation line. Either: a per-paper-agent 5-minute check + one-line justification in the appendix (knock-out), or if the scaling turns out subtly different, it folds into the O1 spike's territory. Lean toward knock-out: spend 10 minutes checking, add the line.

### O8. Sycophancy / activation-engineering literature anchors *(C1, C2, C3)*

**Modest, valuable.** Auditor flags three empirical-LLM-literature gaps:
- *C1 sycophancy* (Sharma et al. 2023, Perez et al. 2022, Wei et al. 2023) — the empirical referent for what the bound captures. One citation in intro framing or conclusion future-directions defuses "where's the empirical motivation?" pushback.
- *C2 activation-engineering* (Zou et al. 2023 *Representation Engineering*, Turner et al. *Activation Addition*) — relevant when activation-mediation idea is introduced for $\kappa$-probing.
- *C3 mechanistic interpretability* (Olsson et al. 2022 *In-context Learning and Induction Heads*) — grounds Lemma 3.5 in empirical attention-pattern observations.

Each is 1 cite + 1 sentence. Cumulative: ~3 sentences across paper. Probably worth doing — directly addresses Codex's "rhetorical surface stronger than formal object" critique by tying the formal object to empirical phenomena it captures.

### O9. Setup density / hypothesis-table / intro citation enumeration *(S1, S3, S4)*

**Defer pending page-budget pressure.** Three suggestions for compression / ergonomics:
- S1 cut citation enumeration in intro paragraphs 1-2 (Strand 1/2 lists already in §F)
- S3 add schematic table mapping (PI/R/K/H1/H2$'$/H4$'$/H$_\kappa$) → which theorem each gates
- S4 move (PI/R/K) axioms out of setup or tag as "Track 2-only"

Body is at 9pp [OK]. Defer until/unless we want compression for some other reason.

### O10. Auditor flagged-as-good — nothing to do *(A6, A8, M8 main, N7, N9, N10, robustness-to-architectural-variants)*

**No-op.** Listed for the record:
- A6: "one channel of hallucination" qualifier in conclusion limitations is the right scope-naming.
- A8: "$\pi/\sqrt 2$ overhead is a *geometric maximum*, not a slack" — right framing.
- M8 main: Lemma 3.5 graph-reachability is "exactly the right grade."
- N7: $0\log 0 = 0$ convention named explicitly.
- N9: double-citation for chain rule on abstract spaces.
- N10: failed-routes appendix.
- "Failed-routes documentation and the three-no-gos disambiguation are model-grade examples of negative-results discipline. I'd protect both from any compression pass." → noted; no compression on those.

### Cosmetic nits *(N2, N4, N6, S5, S6)*

- N2: $\kappa^*$ vs $\kappa_{\text{processing}}^*$ usage consistency
- N4: $(H2')$ vs $(H_2^\prime)$ typesetting consistency
- S5: $\citet$/$\citealt$/$\citep$ usage
- S6: same prime/quote typesetting nit

Lump into an "all-cosmetic-nits-pass" if/when convenient.

### Suggested sequence

1. **Launch O1 spike.** This is the high-leverage item. Three open directions (weaker hypothesis, tighter global, boundary-mapping) — same trichotomy framing as A7. Background, no rush.
2. **Fold O4/O5 into prior knock-out batch** (alongside A3/A4/A7-v + Codex H6).
3. **O2 + O3 + O7** as a separate small commit ("notation hygiene + remainder verification").
4. **O8 sycophancy / activation-engineering / mechanistic-interpretability cites** as a separate connection-finding commit.
5. **O6 future-directions restructure** at the same time as the abstract rewrite (Q1 from peer-feedback queue) — both are positioning moves on the conclusion / abstract.

---

## De-novo audit triage — 2026-05-07 (Codex + Gemini)

Two audits dropped in `audits/`:
- `audits/de_novo_audit_2026_05_06.md` (Gemini, short)
- `audits/de-novo-audit-2026-05-07.md` (Codex, longer; 6 H-tier + 2 M-tier findings)

I read both, verified the load-bearing findings against `src/re/`, and triaged below. **Per AGENTS §3.1, attempted strengthening before accepting any softening recommendation.** Items I'm acting on are ones that survived that test as either (a) honest defects with strengthening paths or (b) genuine over-claims where the strengthening attempt fails.

Items deliberately not surfacing as TODO entries: Gemini's "condense §5 Mechanism" (§5 is doing the OUTLINE-STRATEGY-exemplar narrative-bridge work, not space-saving territory); Gemini's "keep failed routes in appendix" (already done).

### A1. Track 2 √2: clarify finite-local vs limit-asymptotic statement *(real defect, Codex H1)*

**Verified.** Theorem 4.1's Track 2 row says `C = √2`. The proof at `src/re/E-proofs.md:34-49` gives `E d_FR ≤ √2 √I_M (1+o(1))` with **finite, explicit** remainder `R_3(δ_⋆) = (T_⋆/3)·√(2δ_⋆/I_min³)` — non-zero at any δ_⋆ ∈ (0,1), → 0 as δ_⋆ → 0. So at any finite δ_⋆ inside the (H4') regime, the constant is `√(2(1+R_3(δ_⋆)))`, not √2.

**Strengthening attempt (taken).** This isn't a soften — it's a clarify. The cleanest statement: *under (H4'_δ), C(δ) = √(2(1+R(δ)))*, with **R(δ) → 0 as δ → 0** giving locally tight √2 in the limit. That's MORE precise than the current statement, not weaker. Sharpness (Theorem 4.5(b)) then says √2 is the limit-tight bound under (H4').

**Action.** Edit Theorem 4.1's Track 2 row to read along the lines of: "Under (H4') with parameter δ, $C(δ) = \sqrt{2(1+R(δ))}$ with $R(δ) → 0$ as $δ → 0$; **locally tight at √2** in the limit (sharpness via Theorem 4.5(b))." Update §5 mechanism prose to match. Half-paragraph edit at most. Recommended: do.

### A2. Theorem 4.5(b) sharpness witness — Jensen direction wrong *(real defect, Codex H2)*

**Verified.** The sharpness statement claims no `C < √2` bounds `E[d_FR]/√I_M`. The proof at `src/re/E-proofs.md:84-87` shows `E[d_FR²]/I_M → 2` in the conjugate-Gaussian family with `Var_G(β) → 0`. By Jensen, `E[d]² ≤ E[d²]`, so a lower bound on `E[d²]` does *not* propagate to `E[d]`. The proof shows squared-distance sharpness; the theorem claims first-moment sharpness.

**Strengthening attempt.** Two options on the table:
- *(strengthen the witness)* Codex suggests two-point symmetric goal construction: `G ∈ {-a, +a}` equiprobable. By symmetry, `d_FR(P_M|G=+a, P_M)` and `d_FR(P_M|G=-a, P_M)` are equal, so `Var_G(d_FR) = 0` and Jensen is tight. Need to verify the construction lands at `E[d_FR]/√I_M → √2` exactly (the marginal `P_M` becomes a 2-component mixture, not a single Gaussian, so closed-form FR distance isn't immediate — needs one careful computation in the small-`a` limit).
- *(strengthen the theorem statement)* Restate Theorem 4.5(b) for `E[d_FR²]/I_M` directly: "no `C² < 2` bounds `E[d_FR²]/I_M` uniformly across the (H4') regime." That's exactly what the proof shows, and it implies `E[d_FR] ≤ √(E[d_FR²]) ≤ √(2 I_M)·(1+o(1))` by Jensen-the-other-way (which is the upper-bound direction we want). The first-moment claim then follows AS A LIMIT under uniform-locality, not as a finite sharpness.

I lean toward (strengthen the theorem statement) as cleaner — squared-distance sharpness IS what the proof gives, and it's not weaker on the upper-bound side. The witness construction (option 1) might still work but needs spike-level verification I haven't done.

**Action.** Decide between (1) and (2). If (2): one-paragraph rewrite of Theorem 4.5(b) statement + the surrounding Remark. If (1): a small spike in `spikes/` to verify the two-point construction. Recommended: do (2) now, leave (1) as optional follow-up if we want the first-moment statement back.

### A3. κ_processing zero-denominator convention *(real defect, Codex H4)*

**Verified.** Definition at `src/re/03-setup.md:29` gives κ as the ratio of two MIs without specifying the 0/0 case. The text at line 31 handles 0+/0 (parrot, κ=∞) but not 0/0.

**Strengthening attempt.** Not really applicable — this is a small definitional gap, not a softening. The 0/0 case (Class 1 with fully-resolved Ω, no goal info to transfer) gives a trivially-zero bound, and the natural convention is `κ_processing := 0` in that case.

**Action.** Add one sentence after the κ definition at `src/re/03-setup.md:29-31`: *"Convention: when both numerator and denominator are zero (no transferred goal-information and no residual ambiguity), set κ_processing := 0. Then the bound's right-hand side is trivially zero."* Quick fix, do whenever.

### A4. Lemma 3.5 prose-to-formal scope tightening *(real defect, Codex H5)*

**Verified.** Three sites, three different scope-claims:
- `src/re/01-introduction.md:25`: *"every internal computation has a directed-graph path from any input position"* — broadest reading
- `src/re/03-setup.md:23` (table): *"G is causally upstream of every computation"* — also broad
- `src/re/03-setup.md:64-66` (formal lemma): *"for every layer ℓ ≥ 1 and position j ≥ max(i_G ∪ i_E)"* — narrow, downstream-only

The proof's inductive claim at `E-proofs.md:102` is actually broader than the lemma's stated scope (every input position i ≤ j has a path to h_ℓ^(j)) — and the intro prose accurately reflects THAT — but only positions j ≥ max(i_G ∪ i_E) are claimed Coupled-class in the lemma's formal statement.

**Strengthening attempt.** Can the lemma's formal scope be widened to match the prose? For positions j < min(i_G), causal masking blocks the path from goal — those positions are *genuinely* Class 1 (Separated), as noted in the proof's caveat at `E-proofs.md:117`. So no, can't widen. The honest move is to tighten prose.

**Action.** Two edits, both small:
- intro line 25: replace "every internal computation has a directed-graph path from any input position" → "every output computation downstream of the goal positions has a directed-graph path from at least one goal position"
- table row at `03-setup.md:23`: replace "G is causally upstream of every computation" → "G is causally upstream of every downstream output computation"

### A5. Metric uniqueness as forced-choice trajectory *(beauty/wisdom, Gemini #3)*

**Verified by reading.** Currently §4 has Theorem 4.4 (no-go on Euclidean charts) and Theorem 4.5 (Čencov uniqueness + sharpness) as adjacent statements. They flow logically but the *narrative arc* is parallel rather than consequent.

Gemini's reframe: present the sequence as forcing the reader's hand. *"Theorem 4.4 rules out coordinate-naive metrics → (PI)+(R)+(K) carve out the metric space → Čencov's uniqueness within that space picks out Fisher-Rao up-to-scalar → (K) pins the global scalar → √2 is the only surviving constant."* No theorems change; the prose between them gets a single-sentence trajectory frame that makes each step feel inevitable rather than axiomatic.

**Action.** Add a 2-3 sentence narrative bridge between Theorem 4.4 and Theorem 4.5 (probably as the §4.3 opening or as a remark sandwiched between). Could also restructure the existing Remark on alt commitments (TV/Pinsker/Hellinger/χ²/Rényi) to land at the END of the trajectory: *"the no-go tells us exactly what to commit to, the uniqueness tells us exactly what falls out."* The current remark already says this; just sequencing it at the right narrative beat. Beauty pass, ~½-paragraph edit.

### A6. Extend Lemma 3.5 to SSMs / linear-attention? *(strengthening spike, Gemini #4)*

**Maybe.** Mamba/SSM has a recurrent hidden state h_t depending on all past inputs (including goal positions); linear attention has output as a kernel-weighted combination with weights derived from goal-position queries. Both have structural goal-dependence on downstream output computations. The directed-graph-path argument should generalize, but the formalization needs care: "non-degenerate attention" doesn't have a direct analog in SSMs (it's "non-degenerate state-update gain"); linear attention has a different non-degeneracy condition on the kernel.

**Strengthening attempt.** Worth a spike — `spikes/A6-extend-lemma-3.5-to-ssm-linear-attn/` with an investigation. If it works cleanly, generalize Lemma 3.5 to "autoregressive sequence models with goal-dependent hidden states, satisfying a per-architecture non-degeneracy condition." If it doesn't work cleanly, the current narrow form (transformer attention) is fine for the paper's claims and the negative result becomes a pointer-to-future-work.

**Action.** Spike, opus-4.7 model, no rush. Optional but high-value — broadens the bound's applicability without diluting it. Could fold into the paper if it lands cleanly; defer otherwise.

### A7. Track 1 → Stuart-school reduction *(spike PARTIAL — strengthening landed, Codex M2)*

**Status: PARTIAL — strengthening succeeded.** Spike report at `spikes/A7-stuart-school-mapping/report.md` (Opus, 2026-05-07). My initial soften-recommendation in this slot was the AGENTS §3.1 failure mode — once the right transport-inequality lemma was named, a clean theorem-level reduction fell out.

**The result.** Lemma A (Lipschitz pushforward of $T_2$, textbook; Villani 2009 Thm 22.10 / Bobkov-Götze 1999) plus Theorem A7.1' (Class-1 reduction) give a structural mapping: under the canonical Stuart-school hypothesis stack — Lipschitz posterior on the deterministic update map + sub-Gaussian/LSI concentration on the conditional data law — Track 1's $C_{T_2}$ equals $2L_{\text{post}}^2/\rho_{\text{noise}}$, the Stuart-school cascade constant **across the full Strand 2 hypothesis space**, not only the conjugate-Gaussian instance. This sharpens the existing related-work characterization (Hosseini-Hsu-Taghvaei as "closest single-paper match" → all of Strand 2 fits the same structural slot).

**Boundary mapped (failed direction documented).** (SC-strong) — Track 1 reducing every Stuart-school output to a Track-1 corollary — fails for structural reasons (averaged vs pointwise object mismatch, hypothesis-import vs hypothesis-derivation, results outside Track 1's reach: matching lower bounds, multi-metric, sub-Lipschitz, contraction rates, randomized models). §3-§4 of the spike report document the boundary; future agents shouldn't re-attempt without new evidence.

**Honest claim.** *"Track 1 generalizes the Stuart-school cascade across the full Stuart-school hypothesis space"* — neither "strict sub-case" (too strong) nor "conjugate-Gaussian recovery" (too weak).

**Substantive action items from the spike** (each warrants Joseph's read before applying):

- *(A7-i) Replace prose at `src/re/01-introduction.md:17`* — switch "strict sub-case" framing to "generalizes the cascade." Spike §6.1 has the proposed replacement text.
- *(A7-ii) Replace Remark at `src/re/04-main-results.md:30`* — same substitution at theorem-level. Spike §6.2 has the proposed replacement text.
- *(A7-iii) Add `^sec-stuart-school-reduction` subsection to `src/re/E-proofs.md`* — Lemma A + Theorem A7.1' + proofs. ~25-30 lines new appendix material. Spike §2 has the full math.
- *(A7-iv) Sharpen Strand 2 paragraph in `src/re/F-related-work-extended.md`* — make the structural-slot reading explicit instead of single-paper-closest framing. Spike §6.4.
- *(A7-v) Notation clarification at `src/re/C-conjugate-gaussian-numerics.md`* — current `\rho_{\text{LSI}} := 1/\sigma^2` is the noise concentration (Stuart-school cascade denominator), not the LSI constant of the marginal observation law. The math is correct; the symbol-meaning mismatch is worth one-line clarification. Knock-out-sized.

A7-v is small enough to be a knock-out alongside A3/A4. A7-i through A7-iv are substantive — recommend doing them as a single coherent commit ("integrate Stuart-school reduction theorem") since they share a common edit theme.

### Folds-into / no-new-action notes

- *Codex H3 (hallucination size definitional precision)*: folds into existing Q4 ("displacement-not-frequency framing earlier in §1"). The definitional sentence Codex suggests — *"In this paper, hallucination size means the goal-coupling-induced displacement of the model's evidence-conditioned belief state, not the semantic distance from a false output to truth"* — is a clean addition to the §1 Scope reframe planned in Q4.
- *Codex M1 (H1 LLM applicability narrow)*: folds into Q1 (abstract rewrite) and Q4. Both will naturally make the H1-restricted scope of the LLM application visible.
- *Codex H6 ("empirically accessible κ" too strong)*: small fix. Either move sentence at `src/re/04-main-results.md:82` from main text to §6 conclusion's future-work paragraph, or rephrase as "may be empirically probed" rather than "is empirically accessible." Either works; lean toward the rephrase (one-word change). Could do as a knock-out alongside A3/A4.

### Suggested sequence if you say "go"

1. **Knock out A3, A4, A7 + Codex H6 rephrase.** All small surface-level edits, content-preserving (or in A7's case, content-correcting). One commit.
2. **A1 + A2.** The two real Track-2-statement defects. One commit, paired since they're the same axis (theorem statement vs proof).
3. **A5.** Beauty pass on the no-go + uniqueness narrative bridge. Half-paragraph.
4. **A6.** Spike (background, no rush) — extend Lemma 3.5 to SSMs/linear-attention.

A1-A5 should be doable in one sitting if I take a swing at all of them; report back with a diff. A6 is genuinely speculative and warrants its own spike report.

---

## Peer-feedback integration queue — 2026-05-06

Three pieces of peer feedback came in on `paper-rc1.pdf`:
- `audits/peer-review-from-01-tragedy-2026-05-06.md` (paper 1's author)
- `PEER-REVIEW-FROM-B-CS1.md` (paper 2's author)
- "Read-through notes" further down in this file (build-pipeline agent's PDF reading)

Knock-out fixes already landed (commit-pending):

- [x] **Abstract §7.1 forward-ref dropped.** Cut the parenthetical "(positive results showing achievable negligibility exist as a counter-current; §7.1 surveys both directions)" per Joseph's earlier directive in the *Abstract — back-burnered* section below + build-pipeline's confirmation. Minimum-touch fix; full abstract rewrite is item Q1 below.
- [x] **`note:` field hygiene on three bib entries.** Cleared agent-meta `note:` content on `kallenberg-2002-foundations`, `gray-2011-entropy`, `wu-grama-szpankowski-2024`. Build-pipeline confirmed these were leaking working-note text into the rendered bibliography. Verified: `pdftotext out/re-paper.pdf | grep "Cited in\|field-standard\|deferred per source"` returns empty after rebuild.
- [x] **Script-A glyph (𝒜) → `$\mathcal{A}$` sweep in `src/re/`.** Three sites: `01-introduction.md:35`, `04-main-results.md:80`, `B-hypothesis-verification.md:60`. Verified: `grep "Missing character" out/re-paper.log` returns 0 after rebuild. (Build-pipeline flagged this for old `src/`; same glyph was also in `src/re/`.)

Substantive items queued below for your review before I act on them. Items grouped by where the recommendation came from + my own ideas from reading papers 1 and 2.

### Q1. Abstract rewrite — full pass (was back-burnered, now appropriate to take on)

The abstract has been queued for rewrite since the reshape ("see `## Abstract — back-burnered until paper reshape lands` further down). The reshape has now landed. All three peer reviews + your own earlier note converge on the rewrite being the highest-value polish item:

- **Build-pipeline** (read-through note 1): "(positive results showing achievable negligibility...)" is hedge + forward-ref noise — *cut*. *(Done as knock-out, but full rewrite still pending.)*
- **Paper 1 author**: Single paragraph carries five distinct constants ($C$, $\sqrt{2}$, $\pi/\sqrt{2}$, $1/\sqrt{2}$, $L_{\text{post}}\sigma$) plus their conditions. Possible move: leave abstract with umbrella bound + locally-tight $\sqrt{2}$ as the two visible faces; push global $\pi/\sqrt{2}$, Hellinger $1/\sqrt{2}$, and conjugate-Gaussian translation to §1.1 / §4.5.
- **Paper 2 author**: ~14 technical tokens before motivation lands. Front-load the gap (frequency vs size) and the bridging move (chain rule on post-update law) more narratively. Constants and parameter names should appear only after the conceptual picture.
- **Your spec from earlier (in this file below)**: "Target shape: ~5 sentences / ~150 words / one clean question-bound-track-architecture arc" + drop "independent of any architectural-class commitment" + drop conjugate-Gaussian Euclidean detail.

**My recommendation.** Take the rewrite seriously — substantive enough that I want your read on the candidate before pushing. Plan: write 2 candidate abstracts (one Track-2-headline, one Class-ladder-headline per paper 2's Q4 below), commit both to `_abstract-candidates/`, you pick or revise.

### Q2. Class 1/2/3 ladder as organizing principle for the abstract (paper 2's strongest suggestion)

Paper 2's review argues the ladder "is gorgeous and IMO the paper's most durable structural contribution" — possibly *the organizing principle* of the abstract rather than item (1) of four contributions. Their proposed reframe (verbatim from the review):

> "We show that architectures partition into a monotonic ladder of goal-update coupling classes (Separated / Partial / Coupled), and the upper bound `C·√I` applies across the ladder with `κ_processing` automatic for Class 1, named-structural for Class 2, and operational for Class 3 (which includes plain decoder-only transformer attention by construction)."

**My recommendation.** Strong consider. The ladder framing makes the bound a property *of the ladder* rather than a standalone result, which sells the architectural-classification contribution alongside the bound. Risk: makes the paper feel like the ladder is the contribution, with the bound as supporting machinery — which inverts the actual emphasis. Paper 2's author may have read with their own "structural classification" lens (their Regime A/B/C identifiability ladder). **Right answer is probably to write both candidates (Track 2 headline / ladder-organizing) and feel the difference.**

### Q3. Track 2 as headline (paper 2's other big suggestion)

Currently abstract reads "Two routes deliver $C$" — parallel framing. Paper 2's argument: "Track 2 (Fisher-Rao + Čencov) is the paper's *novel* derivation, and Track 1 (transport-inequality cascade) is the connection-to-existing-Stuart-school-literature that demonstrates Track 2's bound is *consistent* with what's already known via a different route." Surfacing Track 2 as headline tightens the contribution narrative.

**My recommendation.** Agree, but want to think about whether the parallel framing was intentional defensive ("not just a Stuart-school refresh"). The novelty story is genuinely Track 2 + the no-go forcing the (PI) commitment. Right answer is folding into Q1 abstract rewrite — Track 2 headline + Track 1 as bridge-to-prior-work + no-go as forcing.

### Q4. Lift "displacement, not frequency" framing earlier in §1 (my idea, inspired by paper 2's §1.2 placement)

Paper 2 puts a §1.2 Scope and Limitations *before* §2 Setup, defining "what 'convergence' means here" before the reader invests in technical machinery. Paper 3 has limitations only in §6 conclusion. The most likely first-pass reader misread is "this is yet another Kalai-Vempala restatement" — addressed by the orthogonal-axes statement in §1's first paragraph, but that statement is currently embedded in a longer Strand-1-then-Strand-2 setup. Lifting the "we bound a *displacement*, not a *frequency*" framing into a more visible position (could be §1.1 Scope subsection, or a dedicated paragraph in §1's opening) would give referees an early off-ramp from the misread.

**My recommendation.** Modest reframe of §1's opening, ~½ paragraph addition or restructuring. Probably worth doing alongside the abstract rewrite (Q1) since both are positioning moves. Should be a self-contained edit.

### Q5. Empirical / concrete instantiation in §4 main body (my idea, inspired by paper 1's Table 1)

Paper 1 has a Table 1 in §4.4 (three-controller drift sweep) — concrete empirical anchor in main body that gives referees a "this is what the result looks like in numbers" hook beyond the math alone. Paper 3's conjugate-Gaussian numerical companion lives in Appendix C; main body has no concrete instantiation. A short "Concrete instantiation" paragraph at end of §4 — ~half-paragraph, no table needed in main body, just pointing to Appendix C with one or two illustrative numbers (e.g., "$L_{\text{post}}\sigma$ bounded by $\tau/2$ uniformly, vanishing in extreme observation-noise limits") — would give the same hook without spending a full table's worth of page-budget.

**My recommendation.** Worth it for referee texture; ~½-paragraph addition in §4 + appropriate cross-ref to Appendix C. Low risk, modest payoff.

### Q6. Parrot architecture parenthetical visibility (paper 1's flag #2)

Paper 1 noticed that the parrot-architecture parenthetical ("$\kappa_{\text{processing}} = \infty$, excluded by scope") in §1 / §3 is doing real work — naming the worst-case witness AND excluding it AND admitting the exclusion — but currently lives mid-sentence where readers will skim past. Their suggestion: lift to a one-paragraph standalone in §1.1 or §3 alongside the (H_κ) introduction.

**My recommendation.** Modest tweak. The parrot architecture is already discussed at appropriate depth in `src/re/B-hypothesis-verification.md` (Appendix B); the question is just whether the §3 forward-pointer to it is visible enough. Could do a one-line restructure: pull "the parrot architecture $M_{\tau^+} := G$ produces $\kappa_{\text{processing}} = \infty$, explicitly outside scope" out of the dense paragraph at `src/re/03-setup.md:31` and give it its own line as a forecasted pointer to Appendix B. Quick fix.

### Q7. Fuller §2 cite-and-distinguish (my idea, inspired by paper 1's §2)

Paper 1's §2 is fuller and more disciplined than paper 3's §2 (paper 3 routes detail to Appendix F to save body pages). Paper 3's §2 is intentionally compressed, but worth re-reading paper 1's §2 as a model when polishing §F.1 / §F.2. Lower priority — only worth touching if Q1-Q6 leave room and the body has page-budget margin.

**My recommendation.** Defer. The compression is a deliberate choice given page budget; paper 1's §2 is right for paper 1's structure. Re-evaluate if §F.1 / §F.2 polish opens up.

### What to act on without further confirmation, vs queue for review

Already done: knock-outs at top of this section.

If you say "go ahead, take a swing at all of Q1-Q6": I'll write 2 abstract candidates (Q1+Q2+Q3 folded together), do Q4 §1 reframe, do Q5 concrete-instantiation paragraph, do Q6 parrot-architecture lift. Defer Q7. Show you a diff before committing.

If you say "just Q1, hold the rest": I'll write the 2 abstract candidates and stop there.

---

## Read-through notes — 2026-05-06 (rc1 = `OUT.re-paper.md`)

Read through `out/re-paper.pdf` carefully — front, several middle pages, last few of main text + references transition. The reshape from 30pp-body to 12pp-body is impressive; spine reads cleanly. A few reactions and suggestions:

**What's working well:**

1. *Title and axis distinction.* "How Much Can LLMs Hallucinate? An Upper Bound via Coupling and Ambiguity" frames the size-vs-frequency axis immediately. Reader knows what to expect within ten words of the title; the orthogonal-axis pivot in line 5-6 of the abstract ("orthogonal — how often versus how much") earns the title's promise.
2. *Hypothesis chain (PI / R / K / H1).* §3.3 staging — Hypothesis 3.1 (PI Sufficient-statistic invariance), 3.2 (R Riemannian structure), 3.3 (K KL second-order matching), 3.4 (H1 Statistical-manifold sub-case) — is exemplary. Each Hypothesis as a numbered amsthm callout with brief motivation between, and the explicit "(R) and (K) are both implicit in any 'E d ≤ C √I' theorem-shape with second-order matching; we name them explicitly so the uniqueness statement of Theorem 4.5 has its hypotheses fully stated" is the right kind of axiom-discipline. This is how Čencov-uniqueness should be staged.
3. *Architectural classification table.* §3.2's Class 1 / 2 / 3 partition with examples reads as a proper mathematical typology rather than three loose buckets — the (Hκ) commitment scope per class (automatic for 1, named for 2/3) makes the architectural reading land. The table renders cleanly in the PDF post-`cols="l X X X"` refactor.
4. *Mechanism § as proof-story not proof-execution.* §5 (Mechanism) sketches Track 1 + Track 2 + the no-go in narrative form, with detailed proofs deferred to appendices A-F. This matches the OUTLINE-STRATEGY.md exemplar pattern (Jin-style: §5 narrates, appendix executes) and is exactly what the 30pp → 9pp reshape is supposed to deliver.

**Suggestions:**

1. *Abstract forward-reference.* Line 3 still has "(positive results showing achievable negligibility exist as a counter-current; §7.1 surveys both directions)" — your earlier TODO note flagged this as a back-burnered post-reshape rewrite, just confirming it's still in the current build. AUTHORING §6.3: "Avoid forward references to section numbers (paper hasn't started yet); name the result instead." A near-equivalent without the section-number could be: "(positive results showing achievable negligibility — Suzuki et al. 2025 — exist as a counter-current; we situate both in our related-work treatment.)" Same content, no forward ref.
2. *Reference field hygiene.* Refs [4] (Wu-Grama-Szpankowski), [19] (Kallenberg), [21] (Gray) all carry author-side working notes in the rendered bibliography — e.g., [4]: "Year-of-record decision (2024 arXiv vs 2025 ICLR) deferred per source OUTLINE — flagged in TODO.md as 'M5 Wu-Grama-Szpankowski venue'." Per AUTHORING §3.9 these are chronicle voice in formal text and shouldn't appear in the submitted PDF. Same systematic issue as 01-tragedy; flagging the underlying `bin/refs emit` filter to the build-pipeline owner separately. In the meantime, the working-note text for those entries can stay in your `bin/refs` working notes elsewhere — just clear the `note:` field of any entry where the value reads as agent-meta rather than scholarly-bibliography.
3. *Lemma 3.5 attention-coupled status.* Cleanly stated and referenced from the table. The "structurally Class 3 by Lemma 3.5, not as an incidental property of training" framing in §6 conclusion lands well.

(*Retraction, 2026-05-06.* I had a fourth suggestion here proposing §3.3 Axioms compression "as a structural lever toward 9pp" — pulled it. That was page-count-driven framing of exactly the kind your VISION.md was written to step back from, and it contradicted my own strengths callout #2 (the four-Hypothesis chain as exemplary axiom-discipline). The Hypothesis chain as it stands is the right reading-shape; if anything moves there, it should move because the spine asks for it, not because of a half-page count.)

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

## Abstract — back-burnered until paper reshape lands (Joseph, 2026-05-06)

The current abstract in `meta.md` reflects the paper's accumulated pre-reshape shape — bolted-on defensive parentheticals, internal-scaffolding qualifiers, three named universal constants where the spine has one, conjugate-Gaussian Euclidean detail, §-number forward-references. Working assumption: rewrite to match the reshaped paper's spine *after* §1–§6 land in `src/re/`. If this means resubmitting a corrected abstract as an OpenReview correction (since the original was submitted 2026-05-05), so be it.

Specific defects already noted for the rewrite:

- First-sentence parenthetical `(positive results showing achievable negligibility exist as a counter-current; §7.1 surveys both directions)` is hedge + forward-ref noise. Cut.
- "under standard regularity conditions and *independent of any architectural-class commitment*" — internal scaffolding. Goes to §4 Main Results, not abstract.
- Three universal constants foregrounded ($\sqrt{2}$ + $\pi/\sqrt{2}$ + $1/\sqrt{2}$). Per VISION.md, only Track 2's $\sqrt{2}$ + the no-go is spine; backstops are appendix.
- Conjugate-Gaussian Euclidean prefactor detail belongs in appendix, not abstract.
- Target shape: ~5 sentences / ~150 words / one clean question-bound-track-architecture arc.

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

---

## Build-pipeline notice — 2026-05-06 (build-pipeline owner)

The umbrella build interface refactored at commit `d24c9e8` (`SPEC-build-refactor.md` for the design discussion). Practical changes you'll see in the working tree on first build:

- **New ephemeral build dir.** `<paper>/.build/<stem>/` replaces `<paper>/out/`. Holds the rendered `.tex`, the auto-emitted `<stem>.references.bib`, lualatex intermediates, and the canonical `<stem>.pdf`. Worth `.gitignore`-ing (`.build/`) when convenient.
- **PDF snapshot-and-swap.** On each build, `<stem>.pdf` moves to `<stem>.prior.pdf` first, then the fresh PDF lands as `<stem>.pdf`. A failed build leaves the prior PDF as the last-known-good. `*.prior.pdf` is also worth `.gitignore`-ing.
- **New tracked artifact.** `<stem>.extracted.bib` is a repo-visibility snapshot of the bib that bibtex actually used. Naming is explicit-on-purpose so it's obvious-by-construction that it's a build artifact (canonical edits go through `bin/refs add` / `refs/entries/<key>.yml`). Recommended to track for diff visibility.
- **`<paper>/refs.bib` is now an orphan.** The build no longer reads or writes it — `bin/refs emit` runs automatically before each compile and writes to `.build/<stem>/<stem>.references.bib`. Existing `<paper>/refs.bib` files just sit there until you remove them.

**One thing surfaced by the new auto-emit flow worth your attention:** three cite-keys in `re-paper`'s segment source resolve against `03-llm-hallucinate-bound/refs.bib` but **not** against `refs/entries/` at the umbrella. Build still produces a PDF (placeholder substitution renders `[?\,key]` for unresolved cites and lints them) but those three references are no longer rendering as proper cites:

  - `tsybakov-2009-nonparametric` — exists as `@book{...}` in your local `refs.bib` but no `refs/entries/<key>.yml`. Run `bin/refs add tsybakov-2009-nonparametric` and paste the BibTeX from your local `refs.bib` (or take a fresh BibTeX from the publisher).
  - `ay-2017-information` — same situation. Run `bin/refs add ay-2017-information` with the BibTeX.
  - `lie-sullivan-teckentrup-2017` — doesn't exist anywhere I could find (not in your local `refs.bib` either). Looks like a typo or a citation that was meant to point at a different key. Worth a search-the-source to figure out what was intended.

The umbrella's `refs/entries/` is the source of truth post-refactor; per-paper `refs.bib` files were the migration artifact. Migrating those last keys closes out the F1.4 paper-side migration entirely.

CLI gained cwd-aware behavior — from inside your paper-dir, `bin/build` (no args) now builds all your manifests. `bin/build <stem>` from cwd builds one. The umbrella forms (`bin/build <paper-dir> [<stem>]`, `bin/build --all`) still work.
