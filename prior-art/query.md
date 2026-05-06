# Undermind Query — B-N8 Logogenic Bias Bound (κ × 𝒜) as Conditional Theorem

**Research question:** Has the meta-claim below — that LLM hallucination bias is bounded as a conditional theorem of the form $\|\Delta M_{\text{bias}}\| \leq C \cdot \kappa \cdot \mathcal{A}$ (architectural coupling × prompt-or-environmental ambiguity), with the constant $C$ derived under explicit named geometric/information-theoretic assumptions, and with a no-go theorem ruling out a universal $C$ under naive Euclidean parameter norm — been derived in any existing framework? Specifically: has anyone formally bounded LLM (or goal-conditioned model) hallucination using transport inequalities (Otto-Villani; Bakry-Émery log-Sobolev) and Lipschitz-posterior-stability arguments, paired with a Fisher-Rao alternative under parameterization-invariance commitments?

This is a focused prior-art investigation seeking a SPECIFIC COMBINATION — most of the constituents are individually well-studied (transport inequalities; Bayesian inverse problems; LLM hallucination heuristics; goal-conditioned RL with belief-goal coupling). What's sought is whether the SPECIFIC COMPOSITION giving a conditional-theorem bound on hallucination as architectural-coupling-times-ambiguity has been derived under any name.

== The claim ==

In Adaptation and Actuation Dynamics (AAD), agents are classified architecturally:
- **Class 1 (modular)**: directed separation by construction. $M_t$ dynamics independent of $O_t/\Sigma_t$. Kalman + LQR fits.
- **Class 2 (fully merged)**: directed separation fails by construction. $\kappa_{\text{processing}} \approx 1$. **LLMs are structurally Class-2** because belief and goal generation couple in the same forward pass.
- **Class 3 (partially modular)**: bounded $\kappa_{\text{processing}}$, partial directed separation.

For Class-2 agents, the directed-separation-violation bias is bounded as a **conditional theorem**:

$$\|\Delta M_{\text{bias}}\| \leq C \cdot \kappa_{\text{processing}} \cdot I(G; \Omega_\tau \mid e_\tau, M_{\tau^-})$$

The rightmost factor is the goal-resolvable residual uncertainty left by the observation — operationally, the *ambiguity* of the prompt or environment.

The constant $C$ — previously order-of-magnitude guidance — was derived in 2026-04-24 as a **conditional theorem under two named tracks**:

**Track 1 (transport-inequality, linear in $I$):** Under three named assumptions — log-Sobolev inequality (Bakry-Émery 1985), Lipschitz-posterior stability (Stuart 2010), Otto-Villani 2000 transport inequality — the constant is:

$$C_{W_2}^2 = \frac{2 L_{\text{post}}^2}{\rho_{\text{LSI}}}$$

with linear-in-$I$ scaling.

**Track 2 (Fisher-Rao, $\sqrt{I}$ scaling):** Under (PI)-parameterization-invariance + Čencov 1982 + small-information regime, the constant is universal and dimension-free:

$$C_{FR} = \sqrt{2}$$

with $\sqrt{I}$ scaling.

**Attempt E no-go:** **No universal $C$ exists under Euclidean-parameter norm.** A heteroscedastic-normal counterexample shows that without a coordinate-invariance commitment, the bound becomes unboundable. This forces the (PI) parameterization-invariance axiom to be load-bearing for theorem-level status — a coordinate-invariance commitment is what lifts the bound from heuristic to theorem. The result is the fourth instance of an identifiability-floor meta-pattern in AAD.

== Distinctive features compared to existing LLM hallucination literature ==

- **Architectural decomposition**: factorizes hallucination into κ (architectural) × 𝒜 (environmental), separately bounding each
- **Conditional-theorem structure**: not a heuristic but a derived bound under explicit named geometric assumptions
- **Two-track formulation**: linear-in-$I$ (transport) and $\sqrt{I}$ (Fisher-Rao) under different geometric commitments
- **No-go theorem ruling out the naive bound**: heteroscedastic-Gaussian counterexample formalizes why coordinate-invariance is required
- **Class-2 formal classification**: gives precise architectural reason why LLMs are structurally subject to hallucination, distinct from "they make mistakes"

== What I'm looking for ==

(a) Has any prior framework formally bounded LLM hallucination using TRANSPORT INEQUALITIES specifically (Otto-Villani / log-Sobolev / Bakry-Émery), as opposed to information-theoretic bounds (Shannon mutual information directly)?

(b) Has any prior framework derived an LLM hallucination bound as a CONDITIONAL THEOREM under named geometric assumptions (vs heuristic / empirical / order-of-magnitude bounds)?

(c) Has the κ × 𝒜 factorization (architectural coupling × ambiguity) been formalized under any name? Specifically: has anyone separated the architectural cause of bias from the environmental cause?

(d) Has the Class 1/2/3 architectural classification (or an equivalent decomposition based on directed-separation-by-construction vs directed-separation-failure) been proposed in LLM theory or goal-conditioned RL?

(e) Has Stuart 2010 Lipschitz-posterior stability been applied to LLM inference or to belief-goal-coupled architectures?

(f) Has the Fisher-Rao / Čencov universal-constant approach been deployed for hallucination bounds, or only for parameter estimation?

(g) Has the heteroscedastic-Gaussian-counterexample-style no-go theorem (showing no universal Euclidean bound exists) been derived in any related formal framework?

== Adjacent formal frameworks worth checking ==

1. **LLM HALLUCINATION THEORY** (Kalai-Vempala 2023 "Calibrated Language Models Must Hallucinate"; Xu-Jain-Kankanhalli 2024 hallucination is inevitable; Manakul-Liusie-Gales 2023 SelfCheckGPT; Lee-Lim-Eisenschlos-Whang 2023 KoLA). Recent formal hallucination work; how do they bound hallucination, and is any bound conditional-theorem-shaped?

2. **POSTERIOR MISSPECIFICATION / BAYESIAN INVERSE PROBLEMS** (Stuart 2010 *Inverse Problems Acta Numerica*; Cotter-Dashti-Stuart 2013; Hairer-Stuart-Vollmer 2014; Mattingly-Pillai-Stuart 2010). Lipschitz-posterior stability is the Stuart 2010 lineage; has this been applied to LLM inference?

3. **TRANSPORT INEQUALITIES** (Otto-Villani 2000 *J. Funct. Anal.*; Talagrand 1996; Ledoux 2004; Bobkov-Götze 1999; Bakry-Émery 1985). Transport inequalities are well-established in probability theory; specific applications to LLM hallucination?

4. **INFORMATION GEOMETRY OF STATISTICAL MODELS** (Amari 1985, 2016; Čencov 1982; Ay-Jost-Lê-Schwachhöfer 2017 *Information Geometry*; Amari-Cichocki 2010). Fisher-Rao + Čencov uniqueness theorems; have these been deployed for hallucination bounds specifically?

5. **GOAL-CONDITIONED RL / BELIEF-GOAL COUPLING** (Schaul-Horgan-Gregor-Silver 2015; Andrychowicz et al. 2017 hindsight experience replay; Eysenbach-Ibarz-Salakhutdinov-Levine 2020; Bi-Held 2021 inverse reinforcement learning interpretation). Goal-conditioned RL has belief-goal coupling; has the directed-separation-violation cost been formalized?

6. **MESA-OPTIMIZATION / INNER ALIGNMENT** (Hubinger-van Merwijk-Mikulik-Skalse-Garrabrant 2019 "Risks from Learned Optimization"; Greenblatt et al. 2024 alignment faking; Hubinger 2020). Mesa-optimization is about learned coupling between belief and goal; has the bias-bound treatment been formalized?

7. **DECEPTIVE ALIGNMENT FORMAL TREATMENTS** (Greenblatt-Denison-Wright et al. 2024; Carlsmith 2023; Soares 2022). Alignment-faking work is empirical; has it been paired with a formal bias bound?

8. **INFORMATION BOTTLENECK APPLIED TO LLMs** (Saxe et al. 2018 information bottleneck in deep learning; Chechik-Globerson-Tishby-Weiss 2005 Gaussian IB; Tishby-Zaslavsky 2015). IB has been applied to neural networks; specific application to LLM bias bounds?

9. **BAYESIAN MODEL ERROR / MODEL MISSPECIFICATION** (Walker 2013; De Blasi-Walker 2013; Kleijn-van der Vaart 2012 misspecified LAN). Bayesian inference under model misspecification; lessons for LLM bias?

10. **NEURAL NETWORK LIPSCHITZ ANALYSIS** (Virmaux-Scaman 2018; Combettes-Pesquet 2020 Lipschitz neural networks). Lipschitz constants of neural networks; applied to LLM posterior stability?

11. **GENERALIZATION BOUNDS VIA TRANSPORT** (Bobkov-Götze; Otto-Villani; Wibisono-Wilson-Jordan 2016 information geometry of gradient flows). Transport inequalities for generalization bounds — has this been carried to LLM hallucination?

12. **CHANNEL CAPACITY / RATE-DISTORTION FOR LANGUAGE MODELS** (Shannon source-coding theorem applied to LLMs). Direct information-theoretic treatments.

== What's already known at targeted-search depth ==

A previous targeted-depth review found:
- LLM hallucination theory has both empirical work and recent formal results (Kalai-Vempala 2023 "must hallucinate") but the formal bounds are typically calibration-style rather than transport-inequality-derived.
- Stuart 2010 Lipschitz-posterior stability is a major Bayesian inverse-problems result; has not been surfaced specifically applied to LLM inference at targeted depth.
- Otto-Villani transport inequalities have been deployed for generalization bounds (Bobkov-Götze line) but not specifically for LLM hallucination as κ × 𝒜.
- Class-1/2/3 architectural classification is AAD-internal; has not been surfaced under another name.
- Mesa-optimization (Hubinger et al. 2019) is the closest neighbor architecturally — about learned belief-goal coupling — but its treatment is empirical-conceptual, not conditional-theorem-shaped.
- The κ × 𝒜 factorization specifically is AAD-internal; has not been surfaced.

The targeted search did NOT pursue: very recent (2024-2026) hallucination theory papers, formal mesa-optimization bounds beyond Hubinger et al. 2019, the Bayesian inverse-problems / posterior-misspecification literature in detail, or the transport-inequality-applied-to-deep-learning literature in detail. These are the high-value directions for a deep search.

== What I want from Undermind ==

A structured prior-art map covering:
1. **Direct anticipation**: any framework with the specific κ × 𝒜 factorization, conditional-theorem structure, and named geometric assumptions
2. **Two-track structure**: anyone deriving both a transport-inequality bound AND a Fisher-Rao bound for the same quantity
3. **No-go for naive bound**: anyone proving the heteroscedastic-counterexample-style result that no universal Euclidean bound exists for hallucination/bias
4. **Architectural decomposition**: any prior architectural classification of LLMs / goal-conditioned models that maps onto Class-1/2/3
5. **Stuart 2010 in LLM**: specific applications of Lipschitz-posterior-stability to LLM inference
6. **Recent 2024-2026 hallucination theory**: state of the art in formal hallucination bounds

Output format: same as the separability-ladder report — direct answer, closest prior-art parallels (ranked), domain-specific findings, naming candidates, evidence register, search scope statement, bottom line.
