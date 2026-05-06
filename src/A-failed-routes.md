## Failed routes ^sec-failed-routes

We document two derivation routes that failed at structural levels, so future work does not re-attempt them without new evidence.

### Route F1: Cramér-Rao inversion ^sec-failed-routes-cramer-rao

**Attempt.** Treat $G$ as a parameter to be estimated from $\Omega$ given $(e, M)$. The Cramér-Rao lower bound gives $\mathrm{Var}(\hat{G}) \geq \mathbf{I}_G^{-1}$ where $\mathbf{I}_G$ is the Fisher information about $G$ given $(\Omega, e, M)$. Invert this to a posterior-sensitivity factor: an upper bound $\Vert\Delta M_{\text{bias}}\Vert \leq L_M \cdot \sqrt{\mathbf{I}_G^{-1}}$ via a Lipschitz-in-$G$ constant on the coupled-update mechanism.

**Why it fails.** Cramér-Rao bounds estimator variance from *below*. To produce an *upper bound* on $\Vert\Delta M_{\text{bias}}\Vert$ via Cramér-Rao inversion would require fixing an estimator class within which $\mathbf{I}_G^{-1}$ is also an upper bound on variance — but no such estimator class exists for the coupled architecture's update mechanism. The mechanism is a deterministic function of $(G, e, M)$, not an estimator of $G$, and there is no uniform-class assumption available. The direction of the Cramér-Rao bound and the direction of the bias bound are opposite; inverting one to the other requires an additional assumption that is not available.

**Lesson.** Information-theoretic *lower-bound* machinery for estimator performance does not invert to upper bounds on side-information-induced displacement.

### Route F2: Rate-distortion inversion ^sec-failed-routes-rate-distortion

**Attempt.** Apply Shannon's rate-distortion inequality $R(D) \geq h(X) - \tfrac{1}{2}\log(2\pi e D)$ for a Gaussian source. Invert to $D \leq \sigma^2 \cdot 2^{-2(R - h(X))}$ with "bits in" interpreted as $I(G;\Omega \mid e, M)$, "distortion" interpreted as $\Vert\Delta M_{\text{bias}}\Vert^2$.

**Why it fails.** Rate-distortion theory describes the minimum bits-per-symbol required to *represent* a source within distortion $D$; it does not describe the maximum *displacement induced* by injecting side-information into an update mechanism. The two problems have different structures: source-coding is about optimal representations; side-information injection is about perturbation propagation. Identifying "bits in" with $I$ and "distortion" with displacement does not produce a sound inequality — the rate-distortion curve is about a different operational quantity.

**Lesson.** Source-coding theorems are about optimal representations of a source, not spatial displacement induced by side-information injection. Upper bounds on displacement require transport-inequality machinery (Pinsker, Otto-Villani, Bakry-Émery, Lipschitz-posterior).

### The pattern ^sec-failed-routes-pattern

Both failed routes attempt to invert *information-theoretic lower-bound* machinery (Cramér-Rao for estimator error; rate-distortion for source coding) into *upper bounds on displacement*. The structural mismatch is uniform: lower-bound machinery for optimization quantities does not invert to upper bounds on perturbation quantities without additional structure that is not available in coupled-architecture settings. Transport-inequality machinery is on the other side of this divide and is the correct family for upper-bound-on-displacement results.
