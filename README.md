# Comment on "Mirrored entanglement witnesses for multipartite and high-dimensional quantum systems"

Author: **Ruqing Chen** — GUT Geoservice Inc., Montreal, Quebec, Canada ·
ORCID [0009-0009-4622-6615](https://orcid.org/0009-0009-4622-6615) · ruqing@hotmail.com

This repository contains a four-page Comment (`comment_qst_2026.pdf`) on

> J. Seong, A. Bera, B. C. Hiesmayr, D. Chruściński, and J. Bae,
> *Mirrored entanglement witnesses for multipartite and high-dimensional quantum systems*,
> Quantum Sci. Technol. **11**, 015037 (2026),
> [doi:10.1088/2058-9565/ae30a3](https://doi.org/10.1088/2058-9565/ae30a3),

together with a deterministic verification script and the figure script. The article is
referred to below as Ref. [1]; all section, page and equation numbers are those of its
published version of record.

## Setting

A mirrored entanglement witness is obtained from a witness W by reflection at its separable
upper bound, M = u_W·1 − W, where u_W is the maximum of ⟨e,f|W|e,f⟩ over product vectors.
The Comment treats the circulant covariant operators on C^n ⊗ C^n

    W_α = Σ_{i,k} α_k |i,i+k⟩⟨i,i+k|  −  Σ_{i≠j} |ii⟩⟨jj|        (indices mod n)

with arbitrary real α = (α_0, …, α_{n−1}); these are the operators of Proposition 5 of
Ref. [1] (Eq. (68)), and for n = 4 the operators W[a,b,c,d] of Eq. (72).

## Results

| Result | Statement |
|---|---|
| **Section 1** – the 4⊗4 example | Section 4.2.1 (p. 25) of Ref. [1] gives the mirror of W[1,1,1,0] as M[1,1,1,0] = (4/3)·1 − W[1,1,1,0]. On the product vector ½(\|0⟩+\|2⟩)⊗(\|0⟩−\|2⟩) one has ⟨W[1,1,1,0]⟩ = 3/2 > 4/3, so ⟨e,f\|M[1,1,1,0]\|e,f⟩ = −1/6: the operator is not an entanglement witness. |
| **Theorem 2** – decomposition certificate | If λ ∈ [0,1], v ≥ α_0 + λ, v ≥ α_k and (v − α_k)(v − α_{n−k}) ≥ (1 − λ)² for all k ≠ 0, then v·1 − W_α = P + Q^Γ with explicit P, Q ≥ 0 (Γ = partial transpose). |
| **Theorem 3** – exact separable bound, every n ≥ 2 | u_W = L_n(α) = max{ α_0, …, α_{n−1}, B_1, …, B_⌊n/2⌋ } with B_k = ((α_0+1)² − α_k α_{n−k}) / (2(α_0+1) − α_k − α_{n−k}), included only if α_0 + 1 > max(α_k, α_{n−k}). The maximum is attained on a product vector supported on at most two levels, and L_n(α)·1 − W_α is decomposable. |
| **Corollary 4** – no non-decomposable mirror | For every n and every real μ: μ·1 − W_α is block positive ⇔ μ ≥ L_n(α) ⇔ μ·1 − W_α is decomposable. In no dimension is a mirrored operator of this family a non-decomposable witness. |
| Consequences for n = 4 | (3/2)·1 − W[1,1,1,0] = 2\|φ⁺⟩⟨φ⁺\| + Q_0^Γ with Q_0 ≥ 0: the correct mirror is decomposable, and Tr[((3/2)·1 − W[1,1,1,0])ρ_x] = 2((x−1)²+2)/x > 0 for the PPT states of Eq. (75). For W[1,…,1,0] the bound is 4/3 for n = 3 and 3/2 for every n ≥ 4. |
| **Proposition 5** – embedding | A non-decomposable mirrored pair (W_3, M_3) in 3⊗3 with W_3 + M_3 = μ·1 yields a non-decomposable mirrored pair in every n⊗n, n ≥ 4, outside the circulant family. |
| Appendix C.4 of Ref. [1] | For the three-qubit state ρ(b,c) of Eq. (64), Tr[W[1,1,0]ρ(b,c)] = 2(c+7)/(b+c+6), not 2(c−3)/(b+c+6): on pp. 36–37 the coefficients r_212 and r_221 have the wrong overall sign and r_122 is given as 0 instead of 4/(b+c+6). Appendix C.3 (Eqs. (131), (133), (134)) is correct and gives the same value. The state is detected by W[1,0,0], W[0,0,1], W[1,0,1], W[1,1,1] for 0 < c < 1. |

## Files

| File | Content |
|---|---|
| `comment_qst_2026.pdf`, `comment_qst_2026.tex` | the Comment (4 pages) and its LaTeX source |
| `verify_mirrored_witnesses.py` | deterministic verification script (85 checks) |
| `verify_output.txt` | complete output of a run of the verification script |
| `make_figures.py` | figure script |
| `fig_negative_region.pdf`, `fig_phase_diagram.pdf` | the two panels of Figure 1 |

## Reproducing the results

Requirements: Python ≥ 3.9 with NumPy and SymPy; Matplotlib for the figures.

```bash
pip install numpy sympy matplotlib
python verify_mirrored_witnesses.py > verify_output.txt
python make_figures.py
```

`verify_mirrored_witnesses.py` prints one `[PASS]`/`[FAIL]` line per check and a summary, and
exits with status 0 if and only if all 85 checks pass (about ninety seconds; last run with
Python 3.12, NumPy 1.26, SymPy 1.13). The decisive checks use exact rational or symbolic
arithmetic; numerical optimization over product vectors is used only as an independent test.
In the script, "SBHCB" abbreviates Ref. [1]. The checks cover:

- **A** – the 4⊗4 example: the value −1/6, the decomposition of (3/2)·1 − W[1,1,1,0], and the
  trace formulas for ρ_x.
- **B** – Theorems 2 and 3: certificate and closed form for n = 3, 4 on random parameters and
  for n = 2, …, 8 in general, with independent numerical maximization over product vectors;
  the two 4⊗4 classes of Ref. [1]; the jump 4/3 → 3/2.
- **C** – recomputation of the other examples of Ref. [1], including the three-qubit states,
  the Pauli coefficients of Appendix C.4 and the block form of Appendix C.3.
- **D** – the embedded pair in 4⊗4 (Proposition 5).

`make_figures.py` writes the figure PDFs next to the script (it also writes
`fig_product_families.pdf`, an illustration of the extremal product vectors that is not used
in the Comment). To rebuild the PDF: `pdflatex comment_qst_2026.tex` (two runs).
