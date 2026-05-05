# LLM Hallucination Upper Bound via Coupling and Ambiguity — paper repository

*An upper bound on LLM bias under coupling and observation ambiguity.* Single-author theory paper. Conditional theorem $\|\Delta M_{\text{bias}}\| \leq C \cdot \kappa_{\text{processing}} \cdot I(G; \Omega \mid e, M)$ under two tracks: transport-inequality (Otto–Villani + Stuart-school posterior stability) and Fisher–Rao geometry (Čencov uniqueness under (PI) parameterization-invariance). No-go theorem rules out universal Euclidean-coordinate constants. Class 1/2/3 architectural classification operationalizes $\kappa_{\text{processing}}$.

Repository follows the segmented-paper workflow: paper segments live in `src/`, with one or more `OUT.*.md` concatenation manifests assembling them into output forms (e.g. `OUT.full-paper.md` for the unconstrained version, `OUT.neurips-2026-paper.md` for the 9-page-budget submission). Currently bootstrapping the segmented layout.

Consumed as a submodule by an umbrella workspace.
