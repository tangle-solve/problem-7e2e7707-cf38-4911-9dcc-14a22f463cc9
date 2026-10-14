<!-- solve-problem:7e2e7707-cf38-4911-9dcc-14a22f463cc9 -->
# Matrix multiplication exponent two

A [Tangle Solve problem](https://solve.tangle.tools/problems/7e2e7707-cf38-4911-9dcc-14a22f463cc9).

## What is the problem?

The matrix multiplication exponent ω is the infimum of exponents τ such that two n×n matrices over a field can be multiplied using O(n^τ) arithmetic operations (additions, subtractions, multiplications, divisions). The formal statement: prove ω = 2, i.e., for every ε > 0 there is an algorithm computing the product of two n×n matrices in O(n^{2+ε}) operations. Standard setting: arithmetic circuits / bilinear algorithms over a field (usually ℂ or any field of characteristic 0; the exponent is field-independent for the techniques used, though this itself is a subtlety). Bilinear complexity of multiplying n×n matrices equals the tensor rank (or more precisely, the asymptotic tensor rank) of the matrix multiplication tensor ⟨n,n,n⟩. Trivially ω ≥ 2 since the output has n² entries. The conjecture is ω = 2. Note the framing "for every ε > 0" — a single algorithm achieving O(n^2 polylog n) would also suffice but is stronger than needed.

## Why does it matter?

Matrix multiplication underlies thousands of algorithms: linear algebra (inversion, determinant, eigendecomposition via fast algorithms), all-pairs shortest paths, transitive closure, parsing, LP interior-point methods, graph matching, and signal processing. Proving ω = 2 would confirm that these can all be done in near-optimal time, and would likely provide the actual algorithms. Conversely, proving ω > 2 would be the first superlinear lower bound for any explicit algebraic problem — either resolution is a landmark in complexity theory.

## What's already known?

- **Upper bounds.** Strassen (1969): ω ≤ log₂7 ≈ 2.808 via a 7-multiplication recursive scheme. The laser method (Strassen 1987; Coppersmith–Winograd 1990) gave ω < 2.376, standing for 20 years. Stothers 2010, Vassilevska Williams 2012, Le Gall 2014 refined it to ~2.373; the group-theoretic approach of Cohn–Umans gave an alternative framework. The current record is ω < 2.371339 (Alman, Duan, Vassilevska Williams, Xu–Zhou 2025 SODA, "More Asymmetry Yields Faster Matrix Multiplication"), using the laser method over asymmetric, higher-power tensor powers.
- **Lower bounds.** Only ω ≥ 2 (output size). Known lower bounds on tensor rank/border rank of ⟨n,n,n⟩ (e.g., Landsberg–Ottaviani style results) are far from n² asymptotically; rank lower bounds for explicit tensors are notoriously stuck around (roughly) 3n or so, and even proving superquadratic rank for any explicit 3-tensor is open (the "FOOHL" barrier, Bläser et al.).
- **Barriers.** Ambainis–Filmus–Regts (2015+) showed the laser method applied to powers of any fixed tensor in the "modular Coppersmith–Winograd family" cannot prove ω = 2 — this is the key obstruction to the current paradigm. The group-theoretic approach hits similar barriers (spectrum-based bounds, Sawin–Tao).

## What would count as solving it?

1. **Positive resolution:** a construction (e.g., a family of tensors, or a direct combinatorial/algorithmic scheme) yielding, for every ε > 0, an O(n^{2+ε}) multiplication algorithm — equivalently a proof that some known family (e.g., powers of a fixed tensor) has asymptotic rank achieving ω = 2. A referee would need an explicit, checkable algorithm or tensor decomposition.
2. **Negative resolution:** a proof that ω > 2, i.e., a superquadratic lower bound on bilinear complexity of matrix multiplication.
3. **Partial but major:** breaking the Ambainis–Filmus–Regts barrier with a genuinely new technique yielding, say, ω = 2 outright via a non-laser-method approach, or proving ω = 2 under a plausible algebraic/geometric conjecture (note: resolution of the cap-set/FLS-style bounds should make one wary of which conjectures are plausible).

## How to start

1. Read Bläser's survey *Fast Matrix Multiplication* (2013, Theory of Computing Graduate Surveys) for the full technical toolkit: Strassen's trick, the laser method, the Schönhage asymptotic sum inequality τ-rank, and the group-theoretic approach.
2. Read the Ambainis–Filmus–Regts barrier paper ("A polynomial bound on the number of different matrix multiplication algorithms produced by the laser method") to understand precisely what the current method cannot do.
3. Read the 2025 record paper (Alman–Duan–Vassilevska Williams–Xu–Zhou) to see the state-of-the-art machinery: asymmetric tensor powers, mixed degeneration schemes.
4. The main obstacle: all known approaches bound ω via "monomial/degeneration structure" of a small fixed tensor, and known barrier results show such approaches saturate strictly above 2. A solver should either find tensors outside barriered families, use geometry (border rank / secant varieties — Landsberg's *Geometry and Complexity Theory*) to get stronger asymptotic decompositions, or find an entirely non-tensorial algorithmic idea.

## Key references

- V. Strassen, "Gaussian Elimination Is Not Optimal," Numerische Mathematik 13 (1969): 354–356. The original 7-multiplication algorithm launching the problem.
- J. Bläser, "Fast Matrix Multiplication," Theory of Computing Graduate Surveys 5 (2013). Comprehensive survey of all techniques: Strassen, laser method, group-theoretic approach. (verify exact volume)
- D. Coppersmith, S. Winograd, "Matrix Multiplication via Arithmetic Progressions," J. Symbolic Computation 9 (1990): 251–280. Introduced the laser method and the tensor that held the record for 20 years.
- A. Ambainis, Y. Filmus, F. Regts, "A polynomial bound on the number of different matrix multiplication algorithms produced by the laser method" (preprint, 2015+; later split into two papers). Proves the laser method on CW-style tensors cannot reach ω = 2. (verify publication venue)
- J. Alman, R. Duan, V. Vassilevska Williams, Y. Xu, Z. Xu, R. Zhou, "More Asymmetry Yields Faster Matrix Multiplication," SODA 2025, DOI: 10.1137/1.9781611978322.63. Current record ω < 2.371339 via asymmetric tensor powers.
- J. M. Landsberg, *Geometry and Complexity Theory*, Cambridge Univ. Press, 2017. Develops the algebraic-geometric viewpoint (border rank, secant varieties) relevant to lower bounds and possible new decompositions.
- H. Cohn, C. Umans, "A Group-theoretic Approach to Fast Matrix Multiplication," FOCS 2003. Alternative framework embedding multiplication into group algebras.

## Warnings

- **Field matters subtly.** Results are typically stated for bilinear complexity over ℂ; transferring to finite fields or general rings requires care (division-free versions exist but change constants).
- **Barrier blindness.** Many attempted papers re-apply the laser method to Coppersmith–Winograd-like tensors without citing Ambainis–Filmus–Regts; such attempts are known to cap at ω > 2.
- **Don't conflate rank and border rank.** The laser method uses degenerations (border rank / asymptotic rank); claimed decompositions must be checked against the correct notion, and small claimed improvements have historically had errors (e.g., retracted claims around 2.3737-type bounds).
- The problem statement "O(n^{2+ε}) for every ε" is strictly weaker than "O(n² polylog n)"; a construction with polylog overhead in the exponent is fine.

---
*`ALGO-000046` · unverified*

## Acceptance guidance

1. **Positive resolution:** a construction (e.g., a family of tensors, or a direct combinatorial/algorithmic scheme) yielding, for every ε > 0, an O(n^{2+ε}) multiplication algorithm — equivalently a proof that some known family (e.g., powers of a fixed tensor) has asymptotic rank achieving ω = 2. A referee would need an explicit, checkable algorithm or tensor decomposition.
2. **Negative resolution:** a proof that ω > 2, i.e., a superquadratic lower bound on bilinear complexity of matrix multiplication.
3. **Partial but major:** breaking the Ambainis–Filmus–Regts barrier with a genuinely new technique yielding, say, ω = 2 outright via a non-laser-method approach, or proving ω = 2 under a plausible algebraic/geometric conjecture (note: resolution of the cap-set/FLS-style bounds should make one wary of which conjectures are plausible).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/7e2e7707-cf38-4911-9dcc-14a22f463cc9?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000046.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000046)
