# Characterization of the Dirichlet-to-Neumann Operator for the Wave Equation

**Academic project carried out during my second year at Mines Nancy, in the Mathematical Engineering department.**

**Project duration**: 9 months (September 2025 – June 2026)

**Author:** Massaro Elias  

**Supervisor:** M. Dos Santos Ferreira (Institut Élie Cartan de Lorraine)

Theoretical and numerical study of the **Dirichlet-to-Neumann (DtN) operator** associated with the wave equation, on three successive geometries (half-space, disc, cylinder), with numerical validation and an inverse problem of geometric reconstruction.


---

## Project overview

The DtN operator assigns to any boundary datum *f* the normal flux of the corresponding solution:

$$\Lambda : f\big|_\Gamma \;\longmapsto\; \partial_\nu u\big|_\Gamma$$

For the wave equation $\partial_t^2 u - \Delta u = 0$, this operator is **pseudodifferential** — its symbol, in Cartesian coordinates on the half-space, equals $\sqrt{s^2 + |\xi'|^2}$ and is not polynomial. Its explicit expression in physical space requires delicate inversion techniques (Bessel/Hankel transforms, distribution theory, Hadamard-Weierstrass factorization, Mittag-Leffler expansion).

The project follows an exploratory approach: each geometry calls for a different inversion strategy, and the report retraces the dead ends, reformulations and successes of every stage.

---

## Project structure

### Chapter 2 — DtN on the half-space

Two independent computations of the kernel of $\Lambda_0$ on $\mathbb{R}^{n-1} \times \mathbb{R}^*_+$:

- **Method 1** — Bessel–Hankel tables and Hadamard finite part: causal kernel in $(t^2 - |x'|^2)^{-3/2}$.
- **Method 2** — Laplacian in the sense of distributions: finite parts of $r^{-3}$ and $r^{-2}$.

The perturbed case (potential *q(x)*) is also treated, via the Lippmann-Schwinger integral equation, the first-order Born approximation and the retarded fundamental solution $E(x,t) = \delta(t-|x|)/(4\pi|x|)$.

### Chapter 3 — DtN on the unit disc

Bounded geometry $\Omega = \{|x| < 1\} \subset \mathbb{R}^2$. The modal symbol is

$$\sigma_n(s) = s \, \frac{I'_n(s)}{I_n(s)}$$

and has poles at the imaginary zeros $\pm i \, j_{n,k}$ of the modified Bessel functions. Direct term-by-term inversion produces a divergent series of Dirac masses. The resolution combines:

- **Hadamard-Weierstrass factorization** of the logarithmic derivative of $I_n$
- **Derivative transfer** ($s^2 \hat{f} = \mathcal{L}\{f''\}$) to make the series absolutely convergent
- Final time-domain expression through convolutions with kernels $\sin(j_{n,k} \, t)/j_{n,k}$

### Chapter 4 — DtN on the finite hollow cylinder *(with numerical validation)*

Cylinder $\Omega = S^1_R \times (0, L)$, with two boundaries $\Gamma_0$ and $\Gamma_L$. The symbol becomes **matrix-valued**:

$$
\widehat{\Lambda}_m(s) =
\begin{pmatrix}
\mu_m \coth(\mu_m L) & -\mu_m / \sinh(\mu_m L) \\
-\mu_m / \sinh(\mu_m L) & \mu_m \coth(\mu_m L)
\end{pmatrix}
$$

where $\mu_m = \sqrt{s^2 + m^2/R^2}$.

The inversion back to the time domain combines:

1. **Mittag-Leffler expansion** of the matrix entries
2. **Derivative transfer** to make the series absolutely convergent
3. Final expression: temporal convolutions with kernels $\sin(\omega_{m,k} \, t)/\omega_{m,k}$, where $\omega_{m,k}^2 = (k\pi/L)^2 + (m/R)^2$

The formula is validated numerically by comparison with a high-resolution finite-difference reference solution (second-order centered scheme, $N_z = 1000$). The agreement is of the order of one percent for the low modes ($m \in \{0,1,2,3\}$), together with a detailed analysis of the degradation at large modes (clustering of the eigenfrequencies, amplification by the mass term, limitation of the reference solution itself).

### Chapter 5 — Inverse problem

Reconstruction of the geometric parameters from knowledge of $\Lambda$ alone:

- **Disc** — Radius *R*: methods based on the static limit or on the eigenfrequencies.
- **Cylinder** — Length *L*: inversion via the diagonal coefficient, via the ratio of the coefficients, or via a high-frequency asymptotic expansion.

---

## Repository contents

```
.
├── Rapport_PR_Elias_Massaro.pdf           # Full research report (6 chapters)
├── validation_cylindre_v2.ipynb           # Jupyter notebook — numerical validation (Chapter 4)
└── README.md
```

---

## Dependencies

```
numpy
matplotlib
jupyter
```

Installation:

```bash
pip install numpy matplotlib jupyter
```

---

## Running the notebook

```bash
jupyter notebook validation_cylindre_v2.ipynb
```

The notebook is self-contained and covers the whole of the Chapter 4 validation: reference solution by finite differences, evaluation of the spectral formula, superimposed comparison for the modes $m \in \{0, 1, 2, 3\}$, convergence study in $k_{\max}$, and analysis of the high-frequency regime ($m \in \{10, 40, 100\}$).
