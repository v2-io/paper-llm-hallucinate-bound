# A6 — Extend Lemma 3.5 to SSMs / linear-attention / autoregressive sequence models

**Status: CRACKED — clean unified statement covers attention + linear attention + selective SSM (Mamba) + RWKV + RetNet + long-convolutions via a single causally-aggregated-mixer abstraction. The directed-graph-path argument is fundamentally architecture-agnostic; "non-degenerate attention weights" is the attention-specific instantiation of a generic per-source non-degeneracy condition (★). Failure modes are catalogued and structurally distinct from the unified case.**

The auditor (Gemini, finding 4) recommended generalizing Lemma 3.5 from "transformer attention" to "autoregressive sequence models with goal-dependent hidden states." The strengthening pass succeeds at the level the auditor pointed at, and a bit beyond: the unified statement is genuinely a *graph-theoretic property of causally-aggregated parameterized DAGs*, of which transformer attention, linear attention, selective SSMs, RWKV, and RetNet are instances under per-architecture non-degeneracy conditions that all reduce to the same structural slot.

---

## 1. The unifying abstraction — causally-aggregated parameterized mixer

The full computational graph of an autoregressive sequence model can be written, layer-by-layer, as

$$h_\ell^{(j)} \;=\; h_{\ell-1}^{(j)} \;+\; F_\ell^{(j)}\bigl(\{h_{\ell-1}^{(i)}\}_{i \le j};\,\theta\bigr) \;+\; G_\ell\bigl(h_{\ell-1}^{(j)};\,\theta\bigr)$$

where:
- The first term is the **same-position residual edge** (always present in modern architectures).
- $F_\ell^{(j)}$ is the **causally-aggregated mixer** — the layer's mechanism for combining information across positions $i \le j$. This is the position-coupling slot.
- $G_\ell$ is **position-wise** — MLPs, normalization, gated MLPs.

The structural claim of `^lem-attention-coupled` depends *only* on:

(R1) **Same-position residual chain** at every layer.

(R2) **Causally-aggregated mixer** $F_\ell^{(j)}$ that takes inputs from $\{h_{\ell-1}^{(i)} : i \le j\}$.

(★) **Per-source non-degeneracy:** for each input position $i \le j$, $\partial F_\ell^{(j)} / \partial h_{\ell-1}^{(i)}$ is generically non-zero on the operating set.

The directed-graph-path argument — induction on layer depth, same-position residual covers $i=j$, cross-position mixer-edge covers $i \ne j$ — is identical in this generic setting. No architecture-specific structure is invoked.

### Strengthened lemma statement

> **Lemma 3.5′ (Coupled-class autoregressive connectivity).** Let $\mathcal{G}_\theta$ be the directed computational graph of an autoregressive sequence model. Suppose at every layer $\ell \ge 1$ each per-position update has the form (R1)+(R2). Let $i_G$ index goal/prompt positions and $i_E$ index evidence positions with $i_G \cap i_E = \emptyset$. Then for every layer $\ell \ge 1$ and position $j \ge \max(i_G \cup i_E)$, $h_\ell^{(j)}$ has a directed-graph path back to every $i_G \le j$, whenever (★) holds along that path.

Same one-induction structure, generic mixer, residual stream covers same-position by default.

---

## 2. Verification of (★) per architecture family

### 2.1 Self-attention (the original Lemma 3.5 case)

Mixer: $F_\ell^{(j)} = \sum_i \alpha_{ji}^{(\ell)}(h_{\ell-1}) V_\ell h_{\ell-1}^{(i)}$ with softmax weights. Per-source partial: $\partial F_\ell^{(j)} / \partial h_{\ell-1}^{(i)} = \alpha_{ji}^{(\ell)} V_\ell$ + softmax-derivative cross-terms. **(★) holds** because softmax is strictly positive ($\alpha_{ji} > 0$) and $V_\ell$ is generically non-singular.

### 2.2 Linear attention (Katharopoulos et al. 2020)

Mixer: $F_\ell^{(j)} = \frac{\sum_{i \le j} \phi(K_\ell h^{(i)})^\top \phi(Q_\ell h^{(j)}) \cdot V_\ell h^{(i)}}{\sum_{i \le j} \phi(K_\ell h^{(i)})^\top \phi(Q_\ell h^{(j)})}$. **(★) holds when $\phi$ is non-vanishing on the operating set.** Standard choices satisfy: $\phi(x) = \mathrm{elu}(x)+1$ (strictly positive), $\phi(x) = \exp(x)$ (RWKV/performer, strictly positive).

### 2.3 Selective state-space models (Mamba / S6, Gu-Dao 2023)

Unrolled: $y_\ell^{(j)} = C_\ell^{(j)} \sum_{i \le j} \bigl(\prod_{k=i+1}^{j} \bar{A}_\ell^{(k)}\bigr) \bar{B}_\ell^{(i)} x_\ell^{(i)}$. Causally-aggregated mixer with leading per-source partial $C_\ell^{(j)} \prod \bar{A} \cdot \bar{B}_\ell^{(i)}$.

**(★) holds** under standard Mamba parameterization: $\bar{A}_\ell^{(k)} = \exp(\Delta_\ell^{(k)} A_\ell)$ with $A_\ell < 0$ diagonal (HiPPO-style), $\Delta_\ell^{(k)} = \mathrm{softplus}(\cdot) > 0$. Eigenvalues lie in $(0,1)$ — non-singular for every $k$. **Mamba's gating is continuous, not binary.** The structural worry — does selective gating "break the path"? — does not materialize. Selectivity is *gain modulation* in a one-parameter family, not a path-cutting routing decision. Quantitative attenuation lives in $\kappa_{\text{processing}}$.

### 2.4 RWKV time-mixing

Mixer: $\mathrm{wkv}_t = \frac{\sum_{i<t} e^{-(t-1-i)w + k_i} v_i + e^{u+k_t} v_t}{\sum_{i<t} e^{-(t-1-i)w+k_i} + e^{u+k_t}}$. Per-source partial contains strictly-positive weight $e^{-(t-1-i)w + k_i}$. **(★) holds.**

### 2.5 RetNet

Mixer: $S_n = \gamma S_{n-1} + k_n^\top v_n$, $y_n = q_n S_n$, with $\gamma \in (0,1)$. Unrolled: $y_n = q_n \sum_{i \le n} \gamma^{n-i} k_i^\top v_i$. **(★) holds.**

### 2.6 Hyena / long-convolution

Mixer: $y_j = \sum_{i \le j} h_{j-i} \cdot x_i$. **(★) holds when the kernel has full causal support.**

---

## 3. Boundary — where (★) fails (Class 2 territory)

**3.1 Hard-routing MoE-attention with goal-conditional routing.** Standard top-$k$ MoE (Switch, Mixtral) is Class 3 — path goes through shared attention layer. The genuine Class 2 case is hypothetical "MoE-attention" where attention itself is expert-routed and goal/output get assigned to disjoint experts.

**3.2 Token-dropping at intermediate layers.** Already in original lemma's caveats.

**3.3 System-level Class 2:** strictly goal-blind retrieval components — LLM stage Class 3, system has Class-1 component.

**3.4 Linear attention with vanishing feature map** ($\phi = \mathrm{ReLU}$ on negative half-space): production architectures avoid by choosing strictly-positive $\phi$.

**3.5 SSM state-collapse** ($\Delta \to \infty$): $\kappa_{\text{processing}}$ phenomenon, not graph-path. Structural Class 3 holds; quantitative usefulness via $\kappa_{\text{processing}}$ is small.

---

## 4. Failed angles

**4.1 Single non-degeneracy condition subsuming all per-architecture variants.** Doesn't add value — per-architecture verifications expose structural features. Per-architecture-corollary form is right.

**4.2 Deriving (★) from training stability / first principles.** Doesn't quite work — training only requires aggregate Jacobian non-zero, not per-source per-position.

**4.3 Stronger graph-theoretic claim — every path non-vanishing.** True but no applicability gain.

**4.4 Tighter (★) — non-zero on positive-measure subset.** Cosmetic; current "generically" framing fine.

**4.5 Searching for a Class-3 architecture outside the unified lemma.** In standard production autoregressive sequence models, no such architecture exists. Only goal-conditional layer skipping (non-standard) escapes.

---

## 5. Bottom line

**Outcome:** Spike-completion state 1 (succeed beyond what we currently claim) — clean unified statement covering attention + linear attention + selective SSMs + RWKV + RetNet + long-convolutions, with per-architecture corollary listing (★) instantiations.

**Key reframing:** Lemma 3.5 is fundamentally a graph-theoretic property of causally-aggregated parameterized DAGs. "Non-degenerate attention weights" is the attention-specific instantiation of (★). The paper currently states the special case; the generic statement is *easier* to prove and broader in applicability.

**Class 2 boundary preserved:** Hard-routing MoE-attention, token-dropping, goal-blind retrieval, vanishing-feature-map linear attention, and SSM state-collapse remain appropriately Class 2 or $\kappa_{\text{processing}}$-attenuated-Class-3.

**Conclusion future-direction language is now stale** — SSMs / linear attention are inside scope, not future work. Reword.

**Diff complexity:** ~100 lines total. Lemma rewrite, corollary added, proof in §E extended with per-architecture verifications, conclusion rephrased, §3 partition-table cell updated.

---

## 6. Caveats

**6.1** The strengthening doesn't extend the *bound's quantitative content*. Lemma 3.5 establishes structural Class 3 — a graph-reachability claim. Quantitative content lives in $\kappa_{\text{processing}}$.

**6.2** (★) can fail on adversarial inputs even for production architectures. The "generically" qualifier covers this in spirit.

**6.3** Class 2 cases listed are not exhaustive. Future architectures may surface cases that don't fit either pattern.

**6.4** The unified abstraction is not novel — graph-theoretic reasoning about computational DAGs is standard. What's novel is recognizing that Lemma 3.5 was *implicitly* a generic graph-theoretic lemma all along.
