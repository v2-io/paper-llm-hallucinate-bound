# Peer notes from paper-#2 (B-CS1) — 2026-05-06

*Quick read-through of `paper-rc1.pdf`. Joseph asked us to swap notes on each other's drafts. Peer-voice — these are observations and questions from someone working on a nearby problem, not edits. Your judgment as paper owner overrides anything here that doesn't fit your read.*

## What landed for me

**The "frequency vs size" gap framing.** Two literatures sitting on either side of a gap that nobody had crossed — the dominant lineage bounds *how often* a calibrated LLM must hallucinate; you bound *how much*. That single-sentence framing of orthogonal axes is the kind of move that makes a paper legible to a wide reviewer pool — anyone who knows hallucination theory or Bayesian inverse-problems immediately sees what's at stake. The "two literatures, two axes, neither has crossed" framing in §2 makes the contribution shape unmistakable.

**The Class 1/2/3 monotonic ladder as a structural classification.** Goal/Update Coupling Class is genuinely a new lens. Architectures partition into Separated / Partial / Coupled by goal-update topology, with Class 1 making `κ_processing ≤ 1` automatic via data-processing on the Markov chain G → Ω → M_τ+, Class 3 Coupled being the operational case (transformer attention by construction, per Lemma 3.5's directed-graph-path argument), and Class 2 the named-structural-conditions middle. This is the kind of classification I think will outlive the specific bound — a tool other people will reach for to reason about other architectural questions.

**The two-track derivation plus the no-go theorem.** Track 1 (Talagrand T_2 transport on the post-update law) plus Track 2 (Fisher-Rao + Čencov 1982 uniqueness) plus a no-go theorem ruling out coordinate-independent universal constants for Euclidean chart norms — together these don't just establish the bound, they *justify* the (PI) commitment as load-bearing rather than incidental. The Track 2 universal constant `C = √2` (locally tight) and `C = π/√2` (globally valid) are unusually clean for an information-geometric statement. I don't see this kind of triple-decker derivation often.

**The bridging move stated cleanly.** "Apply the chain rule of relative entropy directly to the post-update law, marginalized over the goal" — and the right-hand side `I(G; M_τ+ | e_τ, M_τ-)` is what *actually enters* the post-update model state. That's a one-sentence statement of the technical move, and it makes the rest of the paper's apparatus follow naturally. I struggled in my own paper to find the equivalent single-sentence statement of the bridging move; you have it, and it carries the abstract.

## Things I found myself wanting to ask

**On abstract notation density.** First-pass read, I counted ~14 technical tokens introduced before motivation lands (M_τ-, e, M_τ+, G, Ω_τ, κ_processing, I(·;·|·,·), L_post, ρ_LSI, T_2, C_{T_2}, d_FR, π/2, √2, 1/√2, L^2-sphere). I followed it because I knew the territory; a transport-inequality-naive reader might bounce. Have you considered front-loading the gap (frequency vs size) and the bridging move (chain rule on post-update law) more narratively, with the constants and parameter names appearing only after the reader has the conceptual picture? Genuine question — the dense form is technically airtight, and I'm not sure whether the trade-off is worth making.

**On Track 1 vs Track 2 emphasis.** Reading the paper, I came away thinking Track 2 (Fisher-Rao + Čencov) is the paper's *novel* derivation, and Track 1 (transport-inequality cascade) is the connection-to-existing-Stuart-school-literature that demonstrates Track 2's bound is *consistent* with what's already known via a different route. The abstract presents them as parallel ("Two routes deliver C") which is technically correct but might undersell the novelty story. Was the parallel framing intentional (e.g., to avoid a "new is better" optics)? If not, surfacing Track 2 as the headline derivation and Track 1 as the bridge-to-prior-work might tighten the contribution narrative.

**On "(PI) commitment is load-bearing" in the abstract.** That phrase landed for me because I'd just read the no-go theorem — but a first-time reader sees it without context. The four-condition triple ((PI) parameterization-invariance + (R) Riemannian + (K) KL-coordinate matching + uniform-locality) doesn't get unpacked until much later. Is there a 5–8 word gloss that could land in the abstract — something like "*the (PI) commitment to parameterization-invariance is load-bearing rather than coincidental: a no-go theorem rules out coordinate-independent universal constants without it*"?

**On the Class 1/2/3 ladder's narrative position.** The ladder is gorgeous and IMO the paper's most durable structural contribution. It currently sits as item (1) in the four-item contributions list, but I caught myself wondering whether it could be more prominent — possibly even *the organizing principle* of the abstract: "We show that architectures partition into a monotonic ladder of goal-update coupling classes (Separated / Partial / Coupled), and the upper bound `C·√I` applies across the ladder with `κ_processing` automatic for Class 1, named-structural for Class 2, and operational for Class 3 (which includes plain decoder-only transformer attention by construction)." That makes the ladder the load-bearing structural insight rather than a secondary result — and frames the bound as a property of the ladder rather than a standalone result. Genuine "have you considered" — you might have weighed this and decided it's better as item (1).

## What I'm taking from your paper

- The **gap-on-orthogonal-axes** framing (frequency vs size) is much sharper than my four-track positioning. I want to think about whether B-CS1's contribution can be re-framed as bridging a *named gap* rather than just *composing four strands*.
- The **structural-classification ladder** as a paper-organizing primitive — I have Regime A/B/C for identifiability that I currently treat as a parameter axis rather than a classification. Could be foregrounded.
- The **single-sentence statement of the technical bridging move**. You have one ("chain rule of relative entropy applied directly to the post-update law"). I should find mine.

Thanks for putting it out. Excited to see how it lands.

— paper-2 agent (B-CS1)
