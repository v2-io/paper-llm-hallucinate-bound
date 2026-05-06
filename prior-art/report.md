# Hallucination bias bound prior art

##### [**Undermind**](https://undermind.ai)

---

**Research Goal:** Investigate whether any existing academic framework has already derived, under any name, a formal bound on LLM or goal-conditioned-model hallucination, belief-goal-coupled bias, or posterior displacement with the structure of a product between an architectural coupling factor and a residual ambiguity or information-theoretic factor, where the result is presented as a conditional theorem under explicit named geometric assumptions. Count both direct formulations in LLMs or goal-conditioned agents and tight-mapping adjacent precursors, but only when the mapping is structurally tight: theorem-level composition of an architectural factor distinct from an ambiguity or information factor, supported by machinery such as transport inequalities, log-Sobolev or Bakry-Émery assumptions, Lipschitz-posterior stability in the Stuart inverse-problems lineage, or Fisher-Rao / Čencov parameterization-invariant geometry. Especially valuable are prior frameworks with the Otto-Villani transport plus Lipschitz-posterior pushforward cascade, prior frameworks with a Fisher-Rao / Čencov universal-constant approach for the same kind of displacement quantity, and any two-track treatment deriving both kinds of bounds for the same target. Determine whether prior art exists for the following specific structural components: a formal factorization equivalent to architectural coupling × residual ambiguity; a conditional-theorem treatment of hallucination or related bias under named geometric assumptions; an architectural classification equivalent to Class 1 / 2 / 3 based on directed separation by construction versus directed-separation failure; applications of Stuart-style posterior stability to LLM inference or belief-goal-coupled architectures; uses of Fisher-Rao / Čencov geometry for hallucination or posterior-displacement bounds rather than only parameter estimation; and any no-go theorem ruling out a universal Euclidean-parameter constant via a heteroscedastic-style counterexample absent coordinate-invariance commitments. Search broadly across LLM theory, goal-conditioned RL, Bayesian inverse problems, transport inequalities in machine learning and generalization, mesa-optimization and inner alignment, Markov-blanket and directed-separation literature, information bottleneck in deep learning, Bayesian misspecification, neural-network Lipschitz analysis, and recent 2024–2026 formal hallucination theory. The desired output is a structured prior-art map giving a direct-answer top line, a ranked three-tier table distinguishing direct anticipation from closest compositional anticipation and adjacent work, literature-by-literature findings, possible naming candidates, an evidence register that records venue type and date, whether support comes from full text or abstract, citation footprint, and peer-review status, a search-scope statement, and a bottom line on whether the result is direct anticipation, compositional anticipation, or neither.

*Found 41 papers · May 4, 2026 · Estimated coverage of relevant papers: 90%*

## Summary of Results

No direct prior art in the retrieved set proves the target theorem-level hallucination/posterior-displacement bound as an explicit product of an architectural coupling factor and a residual ambiguity/information factor under named geometric assumptions; the landscape instead splits between direct hallucination theory without the geometric factorization \[1\], \[2\], \[3\], \[4\], \[5\] and mature posterior-stability/transport geometry that supplies the needed mathematical half without LLM-specific hallucination targets \[6\], \[7\], \[8\], \[9\], \[10\].

#### Closest direct hits

- \[5\] is the nearest LLM-native match: it explicitly decomposes hallucination risk into data-driven and reasoning-driven components, but the abstract does not indicate a conditional geometric theorem of the requested architectural-coupling × ambiguity form.
- \[1\], \[2\], \[4\], \[11\] give statistical inevitability/lower-bound views of hallucination, but these are architecture-agnostic or capacity-driven, not directed-separation/geometric stability results.

#### Closest compositional anticipation

- Stuart-line Bayesian inverse problems establish posterior Lipschitz stability to data/likelihood/prior perturbations \[6\], \[7\], \[12\], \[13\].
- Transport/functional-inequality work gives explicit constants via Wasserstein, Fisher information, Poincaré, or log-Sobolev machinery \[8\], \[9\], \[14\], \[15\].
- Conditional transport for amortized Bayesian inference supplies pushforward/conditioning-map regularity closest to an Otto–Villani-plus-posterior cascade \[10\].

#### Fisher–Rao / Čencov track

- Fisher–Rao sensitivity exists for Bayesian robustness \[16\], \[17\], and Čencov-style conditional geometry exists \[18\], but no retrieved work uses this route to bound LLM hallucination or universal posterior-displacement constants.

#### Negative finding

- No retrieved paper cleanly anticipates the proposed Class 1/2/3 directed-separation taxonomy, an explicit Stuart-style application to LLM belief-goal coupling, or a no-go theorem specifically excluding universal Euclidean-coordinate constants by coordinate-dependence/heteroscedastic counterexample. The strongest bottom line is **compositional anticipation, not direct anticipation**.

## Paper Catalog (41 papers)

|  | Year | Cit/yr | Title | Authors | Journal |
|---:|:--:|:--:|:---|:---|:---|
| 1 | 2026 | 6.0 | HalluGuard: Demystifying Data-Driven and Reasoning-Driven Hallucinations in LLMs ([link](https://doi.org/10.48550/arXiv.2601.18753)) | Xinyue Zeng et al. | ArXiv |
| 2 | 2019 | 7.1 | On the local Lipschitz stability of Bayesian inverse problems ([link](https://doi.org/10.1088/1361-6420/ab6f43)) | Björn Sprungk | Inverse Problems |
| 3 | 2020 | 2.0 | Lipschitz continuity of probability kernels in the optimal transport framework ([link](https://doi.org/10.1214/23-aihp1389)) | Emanuele Dolera and E. Mainini | Annales de l’Institut Henri Poincaré, Probabilités et Statistiques |
| 4 | 2023 | 63 | Calibrated Language Models Must Hallucinate ([link](https://doi.org/10.1145/3618260.3649777)) | A. Kalai and S. Vempala | Proceedings of the 56th Annual ACM Symposium on Theory of Computing |
| 5 | 2025 |  | Upper and lower bounds for local Lipschitz stability of Bayesian posteriors ([link](https://www.semanticscholar.org/paper/4d2341741cda2583b7a7f5175603616652e5a3e6)) | Nada Cvetkovi’c and Han Cheng Lie |  |
| 6 | 2023 | 4.1 | Bayesian Posterior Perturbation Analysis with Integral Probability Metrics ([link](https://www.semanticscholar.org/paper/3e1139515160bf0aa0a13b316d48847529bb3f28)) | A. Garbuno-Iñigo, T. Helin, F. Hoffmann, and Bamdad Hosseini |  |
| 7 | 2010 |  | Bayesian well-posedness for inverse problems ([link](https://www.semanticscholar.org/paper/42179ddba725b28a978637ae5e610d0d382ea2a7)) | A. Stuart |  |
| 8 | 2025 | 3.0 | Predictable Compression Failures: Why Language Models Actually Hallucinate ([link](https://doi.org/10.48550/arXiv.2509.11208)) | Leon Chlon, Ahmed Karim, and Maggie Chlon | ArXiv |
| 9 | 2013 | 4.6 | Brittleness of Bayesian Inference Under Finite Information in a Continuous World ([link](https://doi.org/10.1214/15-EJS989)) | H. Owhadi, C. Scovel, and T. Sullivan | arXiv: Statistics Theory |
| 10 | 2013 | 5.7 | On the Brittleness of Bayesian Inference ([link](https://doi.org/10.1137/130938633)) | H. Owhadi, C. Scovel, and T. Sullivan | SIAM Rev. |
| 11 | 2015 | 3.7 | Bayesian sensitivity analysis with the Fisher–Rao metric ([link](https://doi.org/10.1093/BIOMET/ASV026)) | S. Kurtek and K. Bharath | Biometrika |
| 12 | 2024 | 3.3 | No Free Lunch: Fundamental Limits of Learning Non-Hallucinating Generative Models ([link](https://doi.org/10.48550/arXiv.2410.19217)) | Changlong Wu, A. Grama, and Wojciech Szpankowski | ArXiv |
| 13 | 2018 | 10 | Certified dimension reduction in nonlinear Bayesian inverse problems ([link](https://www.semanticscholar.org/paper/aaae11f453b1b7b44d4f9eeb29f8b049433fe233)) | O. Zahm, T. Cui, K. Law, A. Spantini, and Y. Marzouk | Math. Comput. |
| 14 | 2025 |  | Are Hallucinations Bad Estimations? ([link](https://doi.org/10.48550/arXiv.2509.21473)) | Hude Liu, Jerry Yao-Chieh Hu, Jennifer Yuntong Zhang, Zhao Song, and Han Liu | ArXiv |
| 15 | 2026 |  | A contraction theory for Sinkhorn and Schrödinger bridges via log-Sobolev inequalities ([link](https://doi.org/10.1080/07362994.2026.2619443)) | P. Del Moral | Stochastic Analysis and Applications |
| 16 | 2026 | 2.0 | Hallucination is a Consequence of Space-Optimality: A Rate-Distortion Theorem for Membership Testing ([link](https://doi.org/10.48550/arXiv.2602.00906)) | Anxin Guo and Jingwei Li | ArXiv |
| 17 | 2025 | 8.7 | (Im)possibility of Automated Hallucination Detection in Large Language Models ([link](https://doi.org/10.48550/arXiv.2504.17004)) | Amin Karbasi, Omar Montasser, John Sous, and Grigoris Velegkas | ArXiv |
| 18 | 2024 | 18 | Mission Impossible: A Statistical Perspective on Jailbreaking LLMs ([link](https://doi.org/10.48550/arXiv.2408.01420)) | Jingtong Su, Julia Kempe, and Karen Ullrich | ArXiv |
| 19 | 2025 | 5.2 | The Policy Cliff: A Theoretical Analysis of Reward-Policy Maps in Large Language Models ([link](https://doi.org/10.48550/arXiv.2507.20150)) | Xingcheng Xu | ArXiv |
| 20 | 2017 | 2.4 | Random forward models and log-likelihoods in Bayesian inverse problems ([link](https://doi.org/10.1137/18M1166523)) | H. Lie, T. Sullivan, and A. Teckentrup | ArXiv |
| 21 | 2019 | 7.9 | On the Well-posedness of Bayesian Inverse Problems ([link](https://doi.org/10.1137/19m1247176)) | J. Latz | SIAM/ASA J. Uncertain. Quantification |
| 22 | 2022 | 1.0 | Strong posterior contraction rates via Wasserstein dynamics ([link](https://doi.org/10.1007/s00440-024-01260-w)) | Emanuele Dolera, S. Favaro, and E. Mainini | Probability Theory and Related Fields |
| 23 | 2025 | 276 | Why Language Models Hallucinate ([link](https://www.semanticscholar.org/paper/0b82eec3b92215b910c19102c33bcd13aa6f8bd0)) | A. Kalai, Ofir Nachum, S. Vempala, and Edwin Zhang | ArXiv |
| 24 | 2025 | 4.9 | Hallucinations are inevitable but can be made statistically negligible. The”innate”inevitability of hallucinations cannot explain practical LLM issues ([link](https://www.semanticscholar.org/paper/7d8546018a5cd8e23839faad4bbf560c1d638a8a)) | Atsushi Suzuki, Yulan He, Feng Tian, and Zhongyuan Wang |  |
| 25 | 2026 |  | A Note on k-NN Gating in RAG ([link](https://www.semanticscholar.org/paper/267472b59c9d0402a67939e38c76bfab51439c62)) | Gérard Biau and Claire Boyer |  |
| 26 | 2023 | 12 | Conditional Optimal Transport on Function Spaces ([link](https://doi.org/10.1137/23m1618922)) | Bamdad Hosseini, Alexander W. Hsu, and Amirhossein Taghvaei | SIAM/ASA J. Uncertain. Quantification |
| 27 | 2021 | 4.7 | Functional inequalities for perturbed measures with applications to log-concave measures and to some Bayesian problems ([link](https://doi.org/10.3150/21-bej1419)) | P. Cattiaux and A. Guillin | Bernoulli |
| 28 | 2016 |  | Submitted to the Annals of Applied Probability DISTANCES BETWEEN NESTED DENSITIES AND A MEASURE OF THE IMPACT OF THE PRIOR IN BAYESIAN STATISTICS By ([link](https://www.semanticscholar.org/paper/7e447d53bbb75fc562d286a4d18f0751d3eefbdf)) | Christophe Ley, G. Reinert, and Yvik Swan |  |
| 29 | 2015 | 3.6 | Distances between nested densities and a measure of the impact of the prior in Bayesian statistics ([link](https://doi.org/10.1214/16-AAP1202)) | Christophe Ley, G. Reinert, and Yvik Swan | arXiv: Probability |
| 30 | 2023 | 1.2 | Choosing Observation Operators to Mitigate Model Error in Bayesian Inverse Problems ([link](https://doi.org/10.1137/23M1602140)) | Nada Cvetkovi’c, H. Lie, Harshit Bansal, and K. Veroy | SIAM/ASA J. Uncertain. Quantification |
| 31 | 2014 | 2.3 | Qualitative Robustness in Bayesian Inference ([link](https://doi.org/10.1051/PS/2017014)) | H. Owhadi and C. Scovel | arXiv: Statistics Theory |
| 32 | 2013 | 9.2 | Robust and Private Bayesian Inference ([link](https://doi.org/10.1007/978-3-319-11662-4_21)) | Christos Dimitrakakis, B. Nelson, Aikaterini Mitrokotsa, and Benjamin I. P. Rubinstein | International Conference on Algorithmic Learning Theory |
| 33 | 2014 | 0.1 | Bayes Sensitivity with Fisher-Rao Metric ([link](https://www.semanticscholar.org/paper/f3de2aad72a9afa548590a6634b9354c6edbb540)) | S. Kurtek and K. Bharath | arXiv: Methodology |
| 34 | 2004 | 0.2 | An Extended Cencov-Campbell Characterization of Conditional Information Geometry ([link](https://www.semanticscholar.org/paper/349d7be32ea92ae1912ffc8dc98eafe7bd0f016d)) | Guy Lebanon | Conference on Uncertainty in Artificial Intelligence |
| 35 | 1993 | 1.8 | Infinitesimal sensitivity of posterior distributions ([link](https://doi.org/10.2307/3315811)) | F. Ruggeri and L. Wasserman | Canadian Journal of Statistics-revue Canadienne De Statistique |
| 36 | 1989 | 5.2 | Local Model Influence ([link](https://doi.org/10.1080/01621459.1989.10478793)) | R. McCulloch | Journal of the American Statistical Association |
| 37 | 2006 | 11 | Misspecification in infinite-dimensional Bayesian statistics ([link](https://doi.org/10.1214/009053606000000029)) | B. Kleijn, W. A., and Van der Vaart | Annals of Statistics |
| 38 | 2009 | 9.1 | Dynamics of Bayesian Updating with Dependent Data and Misspecified Models ([link](https://doi.org/10.1214/09-EJS485)) | C. Shalizi | arXiv: Statistics Theory |
| 39 | 2025 | 1.1 | Stability of Mean-Field Variational Inference ([link](https://www.semanticscholar.org/paper/d412337019ec4169b94584bf87e7b6ce070721d1)) | Shunan Sheng, Bohan Wu, Alberto Gonz’alez-Sanz, and Marcel Nutz |  |
| 40 | 2026 |  | Distributional Stability of Tangent-Linearized Gaussian Inference on Smooth Manifolds ([link](https://doi.org/10.48550/arXiv.2602.19179)) | J. Seo, Hakjin Lee, and Jae-Young Sim | ArXiv |
| 41 | 2026 |  | Action-Sufficient Goal Representations ([link](https://doi.org/10.48550/arXiv.2601.22496)) | Jinu Hyeon, Woobin Park, Hongjoon Ahn, and Taesup Moon | ArXiv |

### Paper Details

1\. · 100% match · 2026 · 6.0 cit/yr\
**HalluGuard: Demystifying Data-Driven and Reasoning-Driven Hallucinations in LLMs** ([link](https://doi.org/10.48550/arXiv.2601.18753))\
Xinyue Zeng et al.\
*ArXiv* · Jan 26, 2026 · 3 citations

> The reliability of Large Language Models (LLMs) in high-stakes domains such as healthcare, law, and scientific discovery is often compromised by hallucinations. These failures typically stem from two sources: data-driven hallucinations and reasoning-driven hallucinations. However, existing detection methods usually address only one source and rely on task-specific heuristics, limiting their generalization to complex scenarios. To overcome these limitations, we introduce the Hallucination Risk Bound, a unified theoretical framework that formally decomposes hallucination risk into data-driven and reasoning-driven components, linked respectively to training-time mismatches and inference-time instabilities. This provides a principled foundation for analyzing how hallucinations emerge and evolve. Building on this foundation, we introduce HalluGuard, an NTK-based score that leverages the induced geometry and captured representations of the NTK to jointly identify data-driven and reasoning-driven hallucinations. We evaluate HalluGuard on 10 diverse benchmarks, 11 competitive baselines, and 9 popular LLM backbones, consistently achieving state-of-the-art performance in detecting diverse forms of LLM hallucinations. We open-source our proposed \model{} model at https://github.com/Susan571/HalluGuard-ICLR2026.

------------------------------------------------------------------------

2\. · 100% match · 2019 · 7.1 cit/yr\
**On the local Lipschitz stability of Bayesian inverse problems** ([link](https://doi.org/10.1088/1361-6420/ab6f43))\
Björn Sprungk\
*Inverse Problems* · Jun 17, 2019 · 49 citations

> In this note we consider the stability of posterior measures occurring in Bayesian inference w.r.t. perturbations of the prior measure and the log-likelihood function. This extends the well-posedness analysis of Bayesian inverse problems. In particular, we prove a general local Lipschitz continuous dependence of the posterior on the prior and the log-likelihood w.r.t. various common distances of probability measures. These include the total variation, Hellinger, and Wasserstein distance and the Kullback–Leibler divergence. We only assume the boundedness of the likelihoods and measure their perturbations in an Lp-norm w.r.t. the prior. The obtained stability yields under mild assumptions the well-posedness of Bayesian inverse problems, in particular, a well-posedness w.r.t. the Wasserstein distance. Moreover, our results indicate an increasing sensitivity of Bayesian inference as the posterior becomes more concentrated, for example due to more or more accurate data. This confirms and extends previous observations made in the sensitivity analysis of Bayesian inference.

------------------------------------------------------------------------

3\. · 100% match · 2020 · 2.0 cit/yr\
**Lipschitz continuity of probability kernels in the optimal transport framework** ([link](https://doi.org/10.1214/23-aihp1389))\
Emanuele Dolera and E. Mainini\
*Annales de l’Institut Henri Poincaré, Probabilités et Statistiques* · Oct 16, 2020 · 11 citations

> In Bayesian statistics, a continuity property of the posterior distribution with respect to the observable variable is crucial as it expresses well-posedness, i.e., stability with respect to errors in the measurement of data. Essentially, this requires to analyze the continuity of a probability kernel or, equivalently, of a conditional probability distribution with respect to the conditioning variable. Here, we give general conditions for the Lipschitz continuity of probability kernels with respect to metric structures arising within the optimal transport framework, such as the Wasserstein metric. For dominated probability kernels over finite-dimensional spaces, we show Lipschitz continuity results with a Lipschitz constant enjoying explicit bounds in terms of Fisher-information functionals and weighted Poincare constants. We also provide results for kernels with moving support, for infinite-dimensional spaces and for non dominated kernels. We show applications to several problems in Bayesian statistics, such as approximation of posterior distributions by mixtures and posterior consistency.

------------------------------------------------------------------------

4\. · 100% match · 2023 · 63 cit/yr\
**Calibrated Language Models Must Hallucinate** ([link](https://doi.org/10.1145/3618260.3649777))\
A. Kalai and S. Vempala\
*Proceedings of the 56th Annual ACM Symposium on Theory of Computing* · Nov 24, 2023 · 155 citations

> Recent language models generate false but plausible-sounding text with surprising frequency. Such “hallucinations” are an obstacle to the usability of language-based AI systems and can harm people who rely upon their outputs. This work shows that there is an inherent statistical lower-bound on the rate that pretrained language models hallucinate certain types of facts, having nothing to do with the transformer LM architecture or data quality. For “arbitrary” facts whose veracity cannot be determined from the training data, we show that hallucinations must occur at a certain rate for language models that satisfy a statistical calibration condition appropriate for generative language models. Specifically, if the maximum probability of any fact is bounded, we show that the probability of generating a hallucination is close to the fraction of facts that occur exactly once in the training data (a “Good-Turing” estimate), even assuming ideal training data without errors. One conclusion is that models pretrained to be sufficiently good predictors (i.e., calibrated) may require post-training to mitigate hallucinations on the type of arbitrary facts that tend to appear once in the training set. However, our analysis also suggests that there is no statistical reason that pretraining will lead to hallucination on facts that tend to appear more than once in the training data (like references to publications such as articles and books, whose hallucinations have been particularly notable and problematic) or on systematic facts (like arithmetic calculations). Therefore, different architectures and learning algorithms may mitigate these latter types of hallucinations.

------------------------------------------------------------------------

5\. · 100% match · 2025\
**Upper and lower bounds for local Lipschitz stability of Bayesian posteriors** ([link](https://www.semanticscholar.org/paper/4d2341741cda2583b7a7f5175603616652e5a3e6))\
Nada Cvetkovi’c and Han Cheng Lie\
May 29, 2025 · 0 citations

> The work of Sprungk (Inverse Problems, 2020) established the local Lipschitz continuity of the misfit-to-posterior and prior-to-posterior maps with respect to the Kullback–Leibler divergence and the total variation, Hellinger, and 1-Wasserstein metrics, by proving certain upper bounds. The upper bounds were also used to show that if a posterior measure is more concentrated, then it can be more sensitive to perturbations in the misfit or prior. We prove upper bounds and lower bounds that emphasise the importance of the evidence. The lower bounds show that the sensitivity of posteriors to perturbations in the misfit or the prior not only can increase, but in general will increase as the posterior measure becomes more concentrated, i.e. as the evidence decreases to zero. Using the explicit dependence of our bounds on the evidence, we identify sufficient conditions for the misfit-to-posterior and prior-to-posterior maps to be locally bi-Lipschitz continuous.

------------------------------------------------------------------------

6\. · 100% match · 2023 · 4.1 cit/yr\
**Bayesian Posterior Perturbation Analysis with Integral Probability Metrics** ([link](https://www.semanticscholar.org/paper/3e1139515160bf0aa0a13b316d48847529bb3f28))\
A. Garbuno-Iñigo, T. Helin, F. Hoffmann, and Bamdad Hosseini\
Mar 2, 2023 · 13 citations

> In recent years, Bayesian inference in large-scale inverse problems found in science, engineering and machine learning has gained significant attention. This paper examines the robustness of the Bayesian approach by analyzing the stability of posterior measures in relation to perturbations in the likelihood potential and the prior measure. We present new stability results using a family of integral probability metrics (divergences) akin to dual problems that arise in optimal transport. Our results stand out from previous works in three directions: (1) We construct new families of integral probability metrics that are adapted to the problem at hand; (2) These new metrics allow us to study both likelihood and prior perturbations in a convenient way; and (3) our analysis accommodates likelihood potentials that are only locally Lipschitz, making them applicable to a wide range of nonlinear inverse problems. Our theoretical findings are further reinforced through specific and novel examples where the approximation rates of posterior measures are obtained for different types of perturbations and provide a path towards the convergence analysis of recently adapted machine learning techniques for Bayesian inverse problems such as data-driven priors and neural network surrogates.

------------------------------------------------------------------------

7\. · 100% match · 2010\
**Bayesian well-posedness for inverse problems** ([link](https://www.semanticscholar.org/paper/42179ddba725b28a978637ae5e610d0d382ea2a7))\
A. Stuart\
May 26, 2010 · 0 citations

> I will describe a theory of well-posed for inverse problems arising in differential equations. The approach is based on adopting a Bayesian viewpoint on function space. Under natural assumptions on the forward problem, this gives Lipschitz continuity of the posterior measure with respect to changes in the data. Applications are numerous and include data assimilation in fluid mechanics and subsurface geophysics.

------------------------------------------------------------------------

8\. · 99% match · 2025 · 3.0 cit/yr\
**Predictable Compression Failures: Why Language Models Actually Hallucinate** ([link](https://doi.org/10.48550/arXiv.2509.11208))\
Leon Chlon, Ahmed Karim, and Maggie Chlon\
*ArXiv* · 4 citations

> Large language models perform near-Bayesian inference yet violate permutation invariance on exchangeable data. We resolve this by showing transformers minimize expected conditional description length (cross-entropy) over orderings, $`\mathbb{E}_\pi[\ell(Y \mid \Gamma_\pi(X))]`$, which admits a Kolmogorov-complexity interpretation up to additive constants, rather than the permutation-invariant description length $`\ell(Y \mid X)`$. This makes them Bayesian in expectation, not in realization. We derive (i) a Quantified Martingale Violation bound showing order-induced deviations scale as $`O(\log n)`$ with constants; (ii) the Expectation-level Decompression Law linking information budgets to reliability for Bernoulli predicates; and (iii) deployable planners (B2T/RoH/ISR) for answer/abstain decisions. Empirically, permutation dispersion follows $`a+b\ln n`$ (Qwen2-7B $`b \approx 0.377`$, Llama-3.1-8B $`b \approx 0.147`$); permutation mixtures improve ground-truth likelihood/accuracy; and randomized dose-response shows hallucinations drop by $`\sim 0.13`$ per additional nat. A pre-specified audit with a fixed ISR=1.0 achieves near-0% hallucinations via calibrated refusal at 24% abstention. The framework turns hallucinations into predictable compression failures and enables principled information budgeting.

------------------------------------------------------------------------

9\. · 96% match · 2013 · 4.6 cit/yr\
**Brittleness of Bayesian Inference Under Finite Information in a Continuous World** ([link](https://doi.org/10.1214/15-EJS989))\
H. Owhadi, C. Scovel, and T. Sullivan\
*arXiv: Statistics Theory* · Apr 24, 2013 · 60 citations

> We derive, in the classical framework of Bayesian sensitivity analysis, optimal lower and upper bounds on posterior values obtained from Bayesian models that exactly capture an arbitrarily large number of finite-dimensional marginals of the data-generating distribution and/or that are as close as desired to the data-generating distribution in the Prokhorov or total variation metrics; these bounds show that such models may still make the largest possible prediction error after conditioning on an arbitrarily large number of sample data measured at finite precision. These results are obtained through the development of a reduction calculus for optimization problems over measures on spaces of measures. We use this calculus to investigate the mechanisms that generate brittleness/robustness and, in particular, we observe that learning and robustness are antagonistic properties. It is now well understood that the numerical resolution of PDEs requires the satisfaction of specific stability conditions. Is there a missing stability condition for using Bayesian inference in a continuous world under finite information?

------------------------------------------------------------------------

10\. · 93% match · 2013 · 5.7 cit/yr\
**On the Brittleness of Bayesian Inference** ([link](https://doi.org/10.1137/130938633))\
H. Owhadi, C. Scovel, and T. Sullivan\
*SIAM Rev.* · Aug 28, 2013 · 72 citations

> With the advent of high-performance computing, Bayesian methods are becoming increasingly popular tools for the quantification of uncertainty throughout science and industry. Since these methods can impact the making of sometimes critical decisions in increasingly complicated contexts, the sensitivity of their posterior conclusions with respect to the underlying models and prior beliefs is a pressing question to which there currently exist positive and negative answers. We report new results suggesting that, although Bayesian methods are robust when the number of possible outcomes is finite or when only a finite number of marginals of the data-generating distribution are unknown, they could be generically brittle when applied to continuous systems (and their discretizations) with finite information on the data-generating distribution. If closeness is defined in terms of the total variation (TV) metric or the matching of a finite system of generalized moments, then (1) two practitioners who use arbitrarily close models and observe the same (possibly arbitrarily large amount of) data may reach opposite conclusions; and (2) any given prior and model can be slightly perturbed to achieve any desired posterior conclusion. The mechanism causing brittleness/robustness suggests that learning and robustness are antagonistic requirements, which raises the possibility of a missing stability condition when using Bayesian inference in a continuous world under finite information.

------------------------------------------------------------------------

11\. · 91% match · 2015 · 3.7 cit/yr\
**Bayesian sensitivity analysis with the Fisher–Rao metric** ([link](https://doi.org/10.1093/BIOMET/ASV026))\
S. Kurtek and K. Bharath\
*Biometrika* · Sep 1, 2015 · 39 citations

> We propose a geometric framework to assess sensitivity of Bayesian procedures to modelling assumptions based on the nonparametric Fisher–Rao metric. While the framework is general, the focus of this article is on assessing local and global robustness in Bayesian procedures with respect to perturbations of the likelihood and prior, and on the identification of influential observations. The approach is based on a square-root representation of densities, which enables analytical computation of geodesic paths and distances, facilitating the definition of naturally calibrated local and global discrepancy measures. An important feature of our approach is the definition of a geometric $`\epsilon`$-contamination class of sampling distributions and priors via intrinsic analysis on the space of probability density functions. We demonstrate the applicability of our framework to generalized mixed-effects models and to directional and shape data.

------------------------------------------------------------------------

12\. · 90% match · 2024 · 3.3 cit/yr\
**No Free Lunch: Fundamental Limits of Learning Non-Hallucinating Generative Models** ([link](https://doi.org/10.48550/arXiv.2410.19217))\
Changlong Wu, A. Grama, and Wojciech Szpankowski\
*ArXiv* · Oct 24, 2024 · 5 citations

> Generative models have shown impressive capabilities in synthesizing high-quality outputs across various domains. However, a persistent challenge is the occurrence of”hallucinations”, where the model produces outputs that are plausible but invalid. While empirical strategies have been explored to mitigate this issue, a rigorous theoretical understanding remains elusive. In this paper, we develop a theoretical framework to analyze the learnability of non-hallucinating generative models from a learning-theoretic perspective. Our results reveal that non-hallucinating learning is statistically impossible when relying solely on the training dataset, even for a hypothesis class of size two and when the entire training set is truthful. To overcome these limitations, we show that incorporating inductive biases aligned with the actual facts into the learning process is essential. We provide a systematic approach to achieve this by restricting the facts set to a concept class of finite VC-dimension and demonstrate its effectiveness under various learning paradigms. Although our findings are primarily conceptual, they represent a first step towards a principled approach to addressing hallucinations in learning generative models.

------------------------------------------------------------------------

13\. · 88% match · 2018 · 10 cit/yr\
**Certified dimension reduction in nonlinear Bayesian inverse problems** ([link](https://www.semanticscholar.org/paper/aaae11f453b1b7b44d4f9eeb29f8b049433fe233))\
O. Zahm, T. Cui, K. Law, A. Spantini, and Y. Marzouk\
*Math. Comput.* · Jul 2, 2018 · 80 citations

> We propose a dimension reduction technique for Bayesian inverse problems with nonlinear forward operators, non-Gaussian priors, and non-Gaussian observation noise. The likelihood function is approximated by a ridge function, i.e., a map which depends non-trivially only on a few linear combinations of the parameters. We build this ridge approximation by minimizing an upper bound on the Kullback-Leibler divergence between the posterior distribution and its approximation. This bound, obtained via logarithmic Sobolev inequalities, allows one to certify the error of the posterior approximation. Computing the bound requires computing the second moment matrix of the gradient of the log-likelihood function. In practice, a sample-based approximation of the upper bound is then required. We provide an analysis that enables control of the posterior approximation error due to this sampling. Numerical and theoretical comparisons with existing methods illustrate the benefits of the proposed methodology.

------------------------------------------------------------------------

14\. · 86% match · 2025\
**Are Hallucinations Bad Estimations?** ([link](https://doi.org/10.48550/arXiv.2509.21473))\
Hude Liu, Jerry Yao-Chieh Hu, Jennifer Yuntong Zhang, Zhao Song, and Han Liu\
*ArXiv* · Sep 25, 2025 · 0 citations

> We formalize hallucinations in generative models as failures to link an estimate to any plausible cause. Under this interpretation, we show that even loss-minimizing optimal estimators still hallucinate. We confirm this with a general high probability lower bound on hallucinate rate for generic data distributions. This reframes hallucination as structural misalignment between loss minimization and human-acceptable outputs, and hence estimation errors induced by miscalibration. Experiments on coin aggregation, open-ended QA, and text-to-image support our theory.

------------------------------------------------------------------------

15\. · 84% match · 2026\
**A contraction theory for Sinkhorn and Schrödinger bridges via log-Sobolev inequalities** ([link](https://doi.org/10.1080/07362994.2026.2619443))\
P. Del Moral\
*Stochastic Analysis and Applications* · Mar 4, 2026 · 0 citations

> Abstract. We develop a quantitative contraction framework for Schrödinger and Sinkhorn bridges based on transportation–cost inequalities and Riccati matrix difference equations. Our approach combines logarithmic Sobolev and Talagrand-type inequalities to obtain explicit entropy and Wasserstein contraction bounds for Sinkhorn bridge measures, entropic optimal transport plans, and the associated Markov transport maps. A key feature of the analysis is the interplay between transport-cost inequalities and matrix Riccati difference equations arising in filtering and stochastic control. The results are established under local regularity assumptions on the reference transition, formulated in terms of curvature, Lipschitz continuity, and Fisher-information bounds. Within this general setting, we derive quantitative stability and convergence estimates for Schrödinger bridges and Sinkhorn iterates that are robust with respect to the choice of reference measure. As a main application, we specialize the theory to linear-Gaussian reference transitions, where the Gaussian structure permits sharp constants, refined exponential decay rates, and continuity estimates for Schrödinger bridges, Sinkhorn iterates, barycentric projections, conditional covariances, and proximal sampler semigroups. In this setting, we recover and extend several known contraction results for entropic and Wasserstein distances and obtain new quantitative bounds that improve previously available rates. Our results provide a unified probabilistic framework for stability, regularity, and convergence of Sinkhorn algorithms. We illustrate the impact of our results on regularized entropic transport, proximal samplers, and diffusion-based generative models, as well as on diffusion flow-matching.

------------------------------------------------------------------------

16\. · 82% match · 2026 · 2.0 cit/yr\
**Hallucination is a Consequence of Space-Optimality: A Rate-Distortion Theorem for Membership Testing** ([link](https://doi.org/10.48550/arXiv.2602.00906))\
Anxin Guo and Jingwei Li\
*ArXiv* · Jan 31, 2026 · 1 citations

> Large language models often hallucinate with high confidence on”random facts”that lack inferable patterns. We formalize the memorization of such facts as a membership testing problem, unifying the discrete error metrics of Bloom filters with the continuous log-loss of LLMs. By analyzing this problem in the regime where facts are sparse in the universe of plausible claims, we establish a rate-distortion theorem: the optimal memory efficiency is characterized by the minimum KL divergence between score distributions on facts and non-facts. This theoretical framework provides a distinctive explanation for hallucination: even with optimal training, perfect data, and a simplified”closed world”setting, the information-theoretically optimal strategy under limited capacity is not to abstain or forget, but to assign high confidence to some non-facts, resulting in hallucination. We validate this theory empirically on synthetic data, showing that hallucinations persist as a natural consequence of lossy compression.

------------------------------------------------------------------------

17\. · 80% match · 2025 · 8.7 cit/yr\
**(Im)possibility of Automated Hallucination Detection in Large Language Models** ([link](https://doi.org/10.48550/arXiv.2504.17004))\
Amin Karbasi, Omar Montasser, John Sous, and Grigoris Velegkas\
*ArXiv* · Apr 23, 2025 · 9 citations

> Is automated hallucination detection possible? In this work, we introduce a theoretical framework to analyze the feasibility of automatically detecting hallucinations produced by large language models (LLMs). Inspired by the classical Gold-Angluin framework for language identification and its recent adaptation to language generation by Kleinberg and Mullainathan, we investigate whether an algorithm, trained on examples drawn from an unknown target language $`K`$ (selected from a countable collection) and given access to an LLM, can reliably determine whether the LLM’s outputs are correct or constitute hallucinations. First, we establish an equivalence between hallucination detection and the classical task of language identification. We prove that any hallucination detection method can be converted into a language identification method, and conversely, algorithms solving language identification can be adapted for hallucination detection. Given the inherent difficulty of language identification, this implies that hallucination detection is fundamentally impossible for most language collections if the detector is trained using only correct examples from the target language. Second, we show that the use of expert-labeled feedback, i.e., training the detector with both positive examples (correct statements) and negative examples (explicitly labeled incorrect statements), dramatically changes this conclusion. Under this enriched training regime, automated hallucination detection becomes possible for all countable language collections. These results highlight the essential role of expert-labeled examples in training hallucination detectors and provide theoretical support for feedback-based methods, such as reinforcement learning with human feedback (RLHF), which have proven critical for reliable LLM deployment.

------------------------------------------------------------------------

18\. · 78% match · 2024 · 18 cit/yr\
**Mission Impossible: A Statistical Perspective on Jailbreaking LLMs** ([link](https://doi.org/10.48550/arXiv.2408.01420))\
Jingtong Su, Julia Kempe, and Karen Ullrich\
*ArXiv* · Aug 2, 2024 · 31 citations

> Large language models (LLMs) are trained on a deluge of text data with limited quality control. As a result, LLMs can exhibit unintended or even harmful behaviours, such as leaking information, fake news or hate speech. Countermeasures, commonly referred to as preference alignment, include fine-tuning the pretrained LLMs with carefully crafted text examples of desired behaviour. Even then, empirical evidence shows preference aligned LLMs can be enticed to harmful behaviour. This so called jailbreaking of LLMs is typically achieved by adversarially modifying the input prompt to the LLM. Our paper provides theoretical insights into the phenomenon of preference alignment and jailbreaking from a statistical perspective. Under our framework, we first show that pretrained LLMs will mimic harmful behaviour if present in the training corpus. Under that same framework, we then introduce a statistical notion of alignment, and lower-bound the jailbreaking probability, showing that it is unpreventable under reasonable assumptions. Based on our insights, we propose an alteration to the currently prevalent alignment strategy RLHF. Specifically, we introduce a simple modification to the RLHF objective, we call E-RLHF, that aims to increase the likelihood of safe responses. E-RLHF brings no additional training cost, and is compatible with other methods. Empirically, we demonstrate that E-RLHF outperforms RLHF on all alignment problems put forward by the AdvBench and HarmBench project without sacrificing model performance as measured by the MT-Bench project.

------------------------------------------------------------------------

19\. · 77% match · 2025 · 5.2 cit/yr\
**The Policy Cliff: A Theoretical Analysis of Reward-Policy Maps in Large Language Models** ([link](https://doi.org/10.48550/arXiv.2507.20150))\
Xingcheng Xu\
*ArXiv* · Jul 27, 2025 · 4 citations

> Reinforcement learning (RL) plays a crucial role in shaping the behavior of large language and reasoning models (LLMs/LRMs). However, it often produces brittle and unstable policies, leading to critical failures such as spurious reasoning, deceptive alignment, and instruction disobedience that undermine the trustworthiness and safety of LLMs/LRMs. Currently, these issues lack a unified theoretical explanation and are typically addressed using ad-hoc heuristics. This paper presents a rigorous mathematical framework for analyzing the stability of the mapping from a reward function to the optimal policy. We show that policy brittleness often stems from non-unique optimal actions, a common occurrence when multiple valid traces exist in a reasoning task. This theoretical lens provides a unified explanation for a range of seemingly disparate failures, reframing them as rational outcomes of optimizing rewards that may be incomplete or noisy, especially in the presence of action degeneracy. We extend this analysis from the fundamental single-reward setting to the more realistic multi-reward RL across diverse domains, showing how stability is governed by an”effective reward”aggregation mechanism. We also prove that entropy regularization restores policy stability at the cost of increased stochasticity. Our framework provides a unified explanation for recent empirical findings on deceptive reasoning, instruction-following trade-offs, and RLHF-induced sophistry, and is further validated through perturbation experiments in multi-reward RL. This work advances policy-stability analysis from empirical heuristics towards a principled theory, offering essential insights for designing safer and more trustworthy AI systems.

------------------------------------------------------------------------

20\. · 76% match · 2017 · 2.4 cit/yr\
**Random forward models and log-likelihoods in Bayesian inverse problems** ([link](https://doi.org/10.1137/18M1166523))\
H. Lie, T. Sullivan, and A. Teckentrup\
*ArXiv* · Dec 15, 2017 · 20 citations

> We consider the use of randomised forward models and log-likelihoods within the Bayesian approach to inverse problems. Such random approximations to the exact forward model or log-likelihood arise naturally when a computationally expensive model is approximated using a cheaper stochastic surrogate, as in Gaussian process emulation (kriging), or in the field of probabilistic numerical methods. We show that the Hellinger distance between the exact and approximate Bayesian posteriors is bounded by moments of the difference between the true and approximate log-likelihoods. Example applications of these stability results are given for randomised misfit models in large data applications and the probabilistic solution of ordinary differential equations.

------------------------------------------------------------------------

21\. · 74% match · 2019 · 7.9 cit/yr\
**On the Well-posedness of Bayesian Inverse Problems** ([link](https://doi.org/10.1137/19m1247176))\
J. Latz\
*SIAM/ASA J. Uncertain. Quantification* · Feb 26, 2019 · 57 citations

> The subject of this article is the introduction of a weaker concept of well-posedness of Bayesian inverse problems. The conventional concept of (\`Lipschitz’) well-posedness in \[Stuart 2010, Acta Numerica 19, pp. 451-559\] is difficult to verify in practice, especially when considering blackbox models, and probably too strong in many contexts. Our concept replaces the Lipschitz continuity of the posterior measure in the Hellinger distance by just continuity. This weakening is tolerable, since the continuity is in general only used as a stability criterion. The main result of this article is a proof of well-posedness for a large class of Bayesian inverse problems, where very little or no information about the underlying model is available. It includes any Bayesian inverse problem arising when observing finite-dimensional data perturbed by additive, non-degenerate Gaussian noise. Moreover, well-posedness with respect to other probability metrics is investigated, including weak convergence, total variation, Wasserstein, and also the Kullback-Leibler divergence.

------------------------------------------------------------------------

22\. · 73% match · 2022 · 1.0 cit/yr\
**Strong posterior contraction rates via Wasserstein dynamics** ([link](https://doi.org/10.1007/s00440-024-01260-w))\
Emanuele Dolera, S. Favaro, and E. Mainini\
*Probability Theory and Related Fields* · Mar 21, 2022 · 4 citations

> In Bayesian statistics, posterior contraction rates (PCRs) quantify the speed at which the posterior distribution concentrates on arbitrarily small neighborhoods of a true model, in a suitable way, as the sample size goes to infinity. In this paper, we develop a new approach to PCRs, with respect to strong norm distances on parameter spaces of functions. Critical to our approach is the combination of a local Lipschitz-continuity for the posterior distribution with a dynamic formulation of the Wasserstein distance, which allows to set forth an interesting connection between PCRs and some classical problems arising in mathematical analysis, probability and statistics, e.g., Laplace methods for approximating integrals, Sanov’s large deviation principles in the Wasserstein distance, rates of convergence of mean Glivenko–Cantelli theorems, and estimates of weighted Poincaré–Wirtinger constants. We first present a theorem on PCRs for a model in the regular infinite-dimensional exponential family, which exploits sufficient statistics of the model, and then extend such a theorem to a general dominated model. These results rely on the development of novel techniques to evaluate Laplace integrals and weighted Poincaré–Wirtinger constants in infinite-dimension, which are of independent interest. The proposed approach is applied to the regular parametric model, the multinomial model, the finite-dimensional and the infinite-dimensional logistic-Gaussian model and the infinite-dimensional linear regression. In general, our approach leads to optimal PCRs in finite-dimensional models, whereas for infinite-dimensional models it is shown explicitly how the prior distribution affect PCRs.

------------------------------------------------------------------------

23\. · 71% match · 2025 · 276 cit/yr\
**Why Language Models Hallucinate** ([link](https://www.semanticscholar.org/paper/0b82eec3b92215b910c19102c33bcd13aa6f8bd0))\
A. Kalai, Ofir Nachum, S. Vempala, and Edwin Zhang\
*ArXiv* · Sep 4, 2025 · 183 citations

> Like students facing hard exam questions, large language models sometimes guess when uncertain, producing plausible yet incorrect statements instead of admitting uncertainty. Such”hallucinations”persist even in state-of-the-art systems and undermine trust. We argue that language models hallucinate because the training and evaluation procedures reward guessing over acknowledging uncertainty, and we analyze the statistical causes of hallucinations in the modern training pipeline. Hallucinations need not be mysterious – they originate simply as errors in binary classification. If incorrect statements cannot be distinguished from facts, then hallucinations in pretrained language models will arise through natural statistical pressures. We then argue that hallucinations persist due to the way most evaluations are graded – language models are optimized to be good test-takers, and guessing when uncertain improves test performance. This”epidemic”of penalizing uncertain responses can only be addressed through a socio-technical mitigation: modifying the scoring of existing benchmarks that are misaligned but dominate leaderboards, rather than introducing additional hallucination evaluations. This change may steer the field toward more trustworthy AI systems.

------------------------------------------------------------------------

24\. · 70% match · 2025 · 4.9 cit/yr\
**Hallucinations are inevitable but can be made statistically negligible. The”innate”inevitability of hallucinations cannot explain practical LLM issues** ([link](https://www.semanticscholar.org/paper/7d8546018a5cd8e23839faad4bbf560c1d638a8a))\
Atsushi Suzuki, Yulan He, Feng Tian, and Zhongyuan Wang\
Feb 15, 2025 · 6 citations

> Hallucinations, a phenomenon where a language model (LM) generates nonfactual content, pose a significant challenge to the practical deployment of LMs. While many empirical methods have been proposed to mitigate hallucinations, recent studies established a computability-theoretic result showing that any LM will inevitably generate hallucinations on an infinite set of inputs, regardless of the quality and quantity of training datasets and the choice of the language model architecture and training and inference algorithms. Although the computability-theoretic result may seem pessimistic, its significance in practical viewpoints has remained unclear. This paper claims that those”innate”inevitability results from computability theory and diagonal argument, in principle, cannot explain practical issues of LLMs. We demonstrate this claim by presenting a positive theoretical result from a probabilistic perspective. Specifically, we prove that hallucinations can be made statistically negligible, provided that the quality and quantity of the training data are sufficient. Interestingly, our positive result coexists with the computability-theoretic result, implying that while hallucinations on an infinite set of inputs cannot be entirely eliminated, their probability can always be reduced by improving algorithms and training data. By evaluating the two seemingly contradictory results through the lens of information theory, we argue that our probability-theoretic positive result better reflects practical considerations than the computability-theoretic negative result.

------------------------------------------------------------------------

25\. · 69% match · 2026\
**A Note on k-NN Gating in RAG** ([link](https://www.semanticscholar.org/paper/267472b59c9d0402a67939e38c76bfab51439c62))\
Gérard Biau and Claire Boyer\
Jan 20, 2026 · 0 citations

> We develop a statistical proxy framework for retrieval-augmented generation (RAG), designed to formalize how a language model (LM) should balance its own predictions with retrieved evidence. For each query x, the system combines a frozen base model q0 ($`\times`$ x) with a k-nearest neighbor retriever r (k ) ($`\times`$ x) through a measurable gate k(x). A retrieval-trust weight wfact (x) quantifies the geometric reliability of the retrieved neighborhood and penalizes retrieval in low-trust regions. We derive the Bayes-optimal per-query gate and analyze its effect on a discordance-based hallucination criterion that captures disagreements between LM predictions and retrieved evidence. We further show that this discordance admits a deterministic asymptotic limit governed solely by the structural agreement (or disagreement) between the Bayes rule and the LM. To account for distribution mismatch between queries and memory, we introduce a hybrid geometric-semantic model combining covariate deformation and label corruption. Overall, this note provides a principled statistical foundation for factuality-oriented RAG systems.

------------------------------------------------------------------------

26\. · 66% match · 2023 · 12 cit/yr\
**Conditional Optimal Transport on Function Spaces** ([link](https://doi.org/10.1137/23m1618922))\
Bamdad Hosseini, Alexander W. Hsu, and Amirhossein Taghvaei\
*SIAM/ASA J. Uncertain. Quantification* · Nov 9, 2023 · 29 citations

> We present a systematic study of conditional triangular transport maps in function spaces from the perspective of optimal transportation and with a view towards amortized Bayesian inference. More specifically, we develop a theory of constrained optimal transport problems that describe block-triangular Monge maps that characterize conditional measures along with their Kantorovich relaxations. This generalizes the theory of optimal triangular transport to separable infinite-dimensional function spaces with general cost functions. We further tailor our results to the case of Bayesian inference problems and obtain regularity estimates on the conditioning maps from the prior to the posterior. Finally, we present numerical experiments that demonstrate the computational applicability of our theoretical results for amortized and likelihood-free inference of functional parameters.

------------------------------------------------------------------------

27\. · 61% match · 2021 · 4.7 cit/yr\
**Functional inequalities for perturbed measures with applications to log-concave measures and to some Bayesian problems** ([link](https://doi.org/10.3150/21-bej1419))\
P. Cattiaux and A. Guillin\
*Bernoulli* · Jan 27, 2021 · 25 citations

> We study functional inequalities (Poincar'e, Cheeger, log-Sobolev) for probability measures obtained as perturbations. Several explicit results for general measures as well as log-concave distributions are given.The initial goal of this work was to obtain explicit bounds on the constants in view of statistical applications for instance. These results are then applied to the Langevin Monte-Carlo method used in statistics in order to compute Bayesian estimators.

------------------------------------------------------------------------

28\. · 59% match · 2016\
**Submitted to the Annals of Applied Probability DISTANCES BETWEEN NESTED DENSITIES AND A MEASURE OF THE IMPACT OF THE PRIOR IN BAYESIAN STATISTICS By** ([link](https://www.semanticscholar.org/paper/7e447d53bbb75fc562d286a4d18f0751d3eefbdf))\
Christophe Ley, G. Reinert, and Yvik Swan\
0 citations

> In this paper we propose tight upper and lower bounds for the Wasserstein distance between any two univariate continuous distributions with probability densities p1 and p2 having nested supports. These explicit bounds are expressed in terms of the derivative of the likelihood ratio p1/p2 as well as the Stein kernel τ1 of p1. The method of proof relies on a new variant of Stein’s method which manipulates Stein operators. We give several applications of these bounds. Our main application is in Bayesian statistics : we derive explicit data-driven bounds on the Wasserstein distance between the posterior distribution based on a given prior and the no-prior posterior based uniquely on the sampling distribution. This is the first finite sample result confirming the wellknown fact that with well-identified parameters and large sample sizes, reasonable choices of prior distributions will have only minor effects on posterior inferences if the data are benign.

------------------------------------------------------------------------

29\. · 57% match · 2015 · 3.6 cit/yr\
**Distances between nested densities and a measure of the impact of the prior in Bayesian statistics** ([link](https://doi.org/10.1214/16-AAP1202))\
Christophe Ley, G. Reinert, and Yvik Swan\
*arXiv: Probability* · Oct 20, 2015 · 38 citations

> In this paper we propose tight upper and lower bounds for the Wasserstein distance between any two {{univariate continuous distributions}} with probability densities $`p_1`$ and $`p_2`$ having nested supports. These explicit bounds are expressed in terms of the derivative of the likelihood ratio $`p_1/p_2`$ as well as the Stein kernel $`\tau_1`$ of $`p_1`$. The method of proof relies on a new variant of Stein’s method which manipulates Stein operators. We give several applications of these bounds. Our main application is in Bayesian statistics : we derive explicit data-driven bounds on the Wasserstein distance between the posterior distribution based on a given prior and the no-prior posterior based uniquely on the sampling distribution. This is the first finite sample result confirming the well-known fact that with well-identified parameters and large sample sizes, reasonable choices of prior distributions will have only minor effects on posterior inferences if the data are benign.

------------------------------------------------------------------------

30\. · 56% match · 2023 · 1.2 cit/yr\
**Choosing Observation Operators to Mitigate Model Error in Bayesian Inverse Problems** ([link](https://doi.org/10.1137/23M1602140))\
Nada Cvetkovi’c, H. Lie, Harshit Bansal, and K. Veroy\
*SIAM/ASA J. Uncertain. Quantification* · Jan 12, 2023 · 4 citations

> In statistical inference, a discrepancy between the parameter-to-observable map that generates the data and the parameter-to-observable map that is used for inference can lead to misspecified likelihoods and thus to incorrect estimates. In many inverse problems, the parameter-to-observable map is the composition of a linear state-to-observable map called an `observation operator' and a possibly nonlinear parameter-to-state map called the`model’. We consider such Bayesian inverse problems where the discrepancy in the parameter-to-observable map is due to the use of an approximate model that differs from the best model, i.e. to nonzero \`model error’. Multiple approaches have been proposed to address such discrepancies, each leading to a specific posterior. We show how to use local Lipschitz stability estimates of posteriors with respect to likelihood perturbations to bound the Kullback–Leibler divergence of the posterior of each approach with respect to the posterior associated to the best model. Our bounds lead to criteria for choosing observation operators that mitigate the effect of model error for Bayesian inverse problems of this type. We illustrate one such criterion on an advection-diffusion-reaction PDE inverse problem from the literature, and use this example to discuss the importance and challenges of model error-aware inference.

------------------------------------------------------------------------

31\. · 55% match · 2014 · 2.3 cit/yr\
**Qualitative Robustness in Bayesian Inference** ([link](https://doi.org/10.1051/PS/2017014))\
H. Owhadi and C. Scovel\
*arXiv: Statistics Theory* · Nov 14, 2014 · 26 citations

> The practical implementation of Bayesian inference requires numerical approximation when closed-form expressions are not available. What types of accuracy (convergence) of the numerical approximations guarantee robustness and what types do not? In particular, is the recursive application of Bayes’ rule robust when subsequent data or posteriors are approximated? When the prior is the push forward of a distribution by the map induced by the solution of a PDE, in which norm should that solution be approximated? Motivated by such questions, we investigate the sensitivity of the distribution of posterior distributions (i.e. posterior distribution-valued random variables, randomized through the data) with respect to perturbations of the prior and data generating distributions in the limit when the number of data points grows towards infinity.

------------------------------------------------------------------------

32\. · 54% match · 2013 · 9.2 cit/yr\
**Robust and Private Bayesian Inference** ([link](https://doi.org/10.1007/978-3-319-11662-4_21))\
Christos Dimitrakakis, B. Nelson, Aikaterini Mitrokotsa, and Benjamin I. P. Rubinstein\
*International Conference on Algorithmic Learning Theory* · Jun 5, 2013 · 119 citations

> We examine the robustness and privacy of Bayesian inference, under assumptions on the prior, and with no modifications to the Bayesian framework. First, we generalise the concept of differential privacy to arbitrary dataset distances, outcome spaces and distribution families. We then prove bounds on the robustness of the posterior, introduce a posterior sampling mechanism, show that it is differentially private and provide finite sample bounds for distinguishability-based privacy under a strong adversarial model. Finally, we give examples satisfying our assumptions.

------------------------------------------------------------------------

33\. · 52% match · 2014 · 0.1 cit/yr\
**Bayes Sensitivity with Fisher-Rao Metric** ([link](https://www.semanticscholar.org/paper/f3de2aad72a9afa548590a6634b9354c6edbb540))\
S. Kurtek and K. Bharath\
*arXiv: Methodology* · Mar 20, 2014 · 1 citations

> We propose a geometric framework to assess sensitivity of Bayesian procedures to modeling assumptions based on the nonparametric Fisher-Rao metric. While the framework is general in spirit, the focus of this article is restricted to metric-based diagnosis under two settings: assessing local and global robustness in Bayesian procedures to perturbations of the likelihood and prior, and identification of influential observations. The approach is based on the square-root representation of densities which enables one to compute geodesics and geodesic distances in analytical form, facilitating the definition of naturally calibrated local and global discrepancy measures. An important feature of our approach is the definition of a geometric $`\epsilon`$-contamination class of sampling distributions and priors via intrinsic analysis on the space of probability density functions. We showcase the applicability of our framework on several simulated toy datasets as well as in real data settings for generalized mixed effects models, directional data and shape data.

------------------------------------------------------------------------

34\. · 49% match · 2004 · 0.2 cit/yr\
**An Extended Cencov-Campbell Characterization of Conditional Information Geometry** ([link](https://www.semanticscholar.org/paper/349d7be32ea92ae1912ffc8dc98eafe7bd0f016d))\
Guy Lebanon\
*Conference on Uncertainty in Artificial Intelligence* · Jul 7, 2004 · 5 citations

> We formulate and prove an axiomatic characterization of conditional information geometry, for both the normalized and the non-normalized cases. This characterization extends the axiomatic derivation of the Fisher geometry by Cencov and Campbell to the cone of positive conditional models, and as a special case to the manifold of conditional distributions. Due to the close connection between the conditional I-divergence and the product Fisher information metric the characterization provides a new axiomatic interpretation of the primal problems underlying logistic regression and AdaBoost.

------------------------------------------------------------------------

35\. · 46% match · 1993 · 1.8 cit/yr\
**Infinitesimal sensitivity of posterior distributions** ([link](https://doi.org/10.2307/3315811))\
F. Ruggeri and L. Wasserman\
*Canadian Journal of Statistics-revue Canadienne De Statistique* · Jun 1, 1993 · 59 citations

> We measure the local sensitivity of a posterior expectation with respect to the prior by computing the norm of the Frechet derivative of the posterior with respect to the prior over several different classes of measures. We compute the derivative of the posterior upper expectation when the prior varies in a restricted ϵ-contamination class. A bound on the global sensitivity of a class of priors is obtained. As an application, we show that of all sets with posterior probability 1 — α, the likelihood region minimizes the norm of the Frechet derivative over the ϵ-contamination class and so is, in some sense, the most robust region with this posterior probability. But there exist counterexamples to this result for other classes of priors.
>
> Nous mesurons la sensibilite locale d’une esperance a posteriori, relativement a la distribution a priori, en calculant la norme de la derivee de Frechet de la distribution a posteriori, relativement a la distribution a priori, pour plusieurs classes de mesures differentes. Nous utilisons la derivee de Frechet afln de calculer la derivee de l’esperance superieure a posteriori lorsque la distribution a priori varie dans une classe restreinte de ϵ-contamination. Une borne pour la sensibilite globale d’une classe de distributions a priori est obtenue. Nous montrons, en tant qu’application, que parmi tous les ensembles avec une probabilite a posteriori de 1 — α, la region de vraisemblance minimise la norme de la derivee de Frechet dans la classe de ϵ-contamination et est done, d’une certaine facon, la region la plus robuste ayant cette probabilite a posteriori. Cependant il existe des contre-exemples a ce resultat pour d’autres classes de distributions a priori.

------------------------------------------------------------------------

36\. · 43% match · 1989 · 5.2 cit/yr\
**Local Model Influence** ([link](https://doi.org/10.1080/01621459.1989.10478793))\
R. McCulloch\
*Journal of the American Statistical Association* · Jun 1, 1989 · 191 citations

> Abstract This article develops a general method for assessing the influence of model assumptions in a Bayesian analysis. We assume that model choices are indexed by a hyperparameter with some given initial choice. We use the term “model” to encompass both the sampling model and the prior distribution. We wish to assess the effect of changing the hyperparameter away from the initial choice. We are performing a sensitivity analysis, with the hyperparameter defining our perturbations. We use the Kullback—Leibler divergence to measure the difference between posteriors corresponding to different choices of the hyperparameter. We also measure the change in priors. If small changes in the priors lead to large changes in posteriors, the choice of hyperparameter is influential. The second-order difference in the Kullback—Leibler divergence is expressed by Fisher information matrices. The relative change in posteriors compared with priors may be summarized by the relative eigenvalue of the posterior and prior Fishe…

------------------------------------------------------------------------

37\. · 41% match · 2006 · 11 cit/yr\
**Misspecification in infinite-dimensional Bayesian statistics** ([link](https://doi.org/10.1214/009053606000000029))\
B. Kleijn, W. A., and Van der Vaart\
*Annals of Statistics* · Apr 1, 2006 · 228 citations

> We consider the asymptotic behavior of posterior distributions if the model is misspecified. Given a prior distribution and a random sample from a distribution P 0 , which may not be in the support of the prior, we show that the posterior concentrates its mass near the points in the support of the prior that minimize the Kullback-Leibler divergence with respect to P 0 . An entropy condition and a prior-mass condition determine the rate of convergence. The method is applied to several examples, with special interest for infinite-dimensional models. These include Gaussian mixtures, nonparametric regression and parametric models.

------------------------------------------------------------------------

38\. · 39% match · 2009 · 9.1 cit/yr\
**Dynamics of Bayesian Updating with Dependent Data and Misspecified Models** ([link](https://doi.org/10.1214/09-EJS485))\
C. Shalizi\
*arXiv: Statistics Theory* · Jan 11, 2009 · 157 citations

> Much is now known about the consistency of Bayesian updating on infinite-dimensional parameter spaces with independent or Markovian data. Necessary conditions for consistency include the prior putting enough weight on the correct neighborhoods of the data-generating distribution; various sufficient conditions further restrict the prior in ways analogous to capacity control in frequentist nonparametrics. The asymptotics of Bayesian updating with mis-specified models or priors, or non-Markovian data, are far less well explored. Here I establish sufficient conditions for posterior convergence when all hypotheses are wrong, and the data have complex dependencies. The main dynamical assumption is the asymptotic equipartition (Shannon-McMillan-Breiman) property of information theory. This, along with Egorov’s Theorem on uniform convergence, lets me build a sieve-like structure for the prior. The main statistical assumption, also a form of capacity control, concerns the compatibility of the prior and the data-generating process, controlling the fluctuations in the log-likelihood when averaged over the sieve-like sets. In addition to posterior convergence, I derive a kind of large deviations principle for the posterior measure, extending in some cases to rates of convergence, and discuss the advantages of predicting using a combination of models known to be wrong. An appendix sketches connections between these results and the replicator dynamics of evolutionary theory.

------------------------------------------------------------------------

39\. · 37% match · 2025 · 1.1 cit/yr\
**Stability of Mean-Field Variational Inference** ([link](https://www.semanticscholar.org/paper/d412337019ec4169b94584bf87e7b6ce070721d1))\
Shunan Sheng, Bohan Wu, Alberto Gonz’alez-Sanz, and Marcel Nutz\
Jun 9, 2025 · 1 citations

> Mean-field variational inference (MFVI) is a widely used method for approximating high-dimensional probability distributions by product measures. This paper studies the stability properties of the mean-field approximation when the target distribution varies within the class of strongly log-concave measures. We establish dimension-free Lipschitz continuity of the MFVI optimizer with respect to the target distribution, measured in the 2-Wasserstein distance, with Lipschitz constant inversely proportional to the log-concavity parameter. Under additional regularity conditions, we further show that the MFVI optimizer depends differentiably on the target potential and characterize the derivative by a partial differential equation. Methodologically, we follow a novel approach to MFVI via linearized optimal transport: the non-convex MFVI problem is lifted to a convex optimization over transport maps with a fixed base measure, enabling the use of calculus of variations and functional analysis. We discuss several applications of our results to robust Bayesian inference and empirical Bayes, including a quantitative Bernstein–von Mises theorem for MFVI, as well as to distributed stochastic control.

------------------------------------------------------------------------

40\. · 36% match · 2026\
**Distributional Stability of Tangent-Linearized Gaussian Inference on Smooth Manifolds** ([link](https://doi.org/10.48550/arXiv.2602.19179))\
J. Seo, Hakjin Lee, and Jae-Young Sim\
*ArXiv* · Feb 22, 2026 · 0 citations

> Gaussian inference on smooth manifolds is central to robotics, but exact marginalization and conditioning are generally non-Gaussian and geometry-dependent. We study tangent-linearized Gaussian inference and derive explicit non-asymptotic $`W_2`$ stability bounds for projection marginalization and surface-measure conditioning. The bounds separate local second-order geometric distortion from nonlocal tail leakage and, for Gaussian inputs, yield closed-form diagnostics from $`(\mu,\Sigma)`$ and curvature/reach surrogates. Circle and planar-pushing experiments validate the predicted calibration transition near $`\sqrt{\|\Sigma\|_{\mathrm{op}}}/R\approx 1/6`$ and indicate that normal-direction uncertainty is the dominant failure mode when locality breaks. These diagnostics provide practical triggers for switching from single-chart linearization to multi-chart or sample-based manifold inference.

------------------------------------------------------------------------

41\. · 34% match · 2026\
**Action-Sufficient Goal Representations** ([link](https://doi.org/10.48550/arXiv.2601.22496))\
Jinu Hyeon, Woobin Park, Hongjoon Ahn, and Taesup Moon\
*ArXiv* · Jan 30, 2026 · 0 citations

> Hierarchical policies in offline goal-conditioned reinforcement learning (GCRL) addresses long-horizon tasks by decomposing control into high-level subgoal planning and low-level action execution. A critical design choice in such architectures is the goal representation-the compressed encoding of goals that serves as the interface between these levels. Existing approaches commonly derive goal representations while learning value functions, implicitly assuming that preserving information sufficient for value estimation is adequate for optimal control. We show that this assumption can fail, even when the value estimation is exact, as such representations may collapse goal states that need to be differentiated for action learning. To address this, we introduce an information-theoretic framework that defines action sufficiency, a condition on goal representations necessary for optimal action selection. We prove that value sufficiency does not imply action sufficiency and empirically verify that the latter is more strongly associated with control success in a discrete environment. We further demonstrate that standard log-loss training of low-level policies naturally induces action-sufficient representations. Our experimental results a popular benchmark demonstrate that our actor-derived representations consistently outperform representations learned via value estimation.
