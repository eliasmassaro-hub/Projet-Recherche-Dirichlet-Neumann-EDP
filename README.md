# Caractérisation de l'opérateur Dirichlet-à-Neumann pour l'équation des ondes

**Projet académique mené pendant ma 2ème année aux Mines de Nancy en département Ingénierie Mathématique.**
**Durée du projet**: 9 mois (sept 2025 - juin 2026)
**Encadrant :** M. Dos Santos Ferreira (Institut Élie Cartan de Lorraine)
Étude théorique et numérique de l'**opérateur Dirichlet-à-Neumann (DtN)** associé à l'équation des ondes, sur trois géométries successives (demi-espace, disque, cylindre), avec validation numérique et problème inverse de reconstruction géométrique.

**Auteur :** Massaro Elias — 
---

## Présentation du projet

L'opérateur DtN associe à toute donnée au bord *f* le flux normal de la solution correspondante :

$$\Lambda : f\big|_\Gamma \;\longmapsto\; \partial_\nu u\big|_\Gamma$$

Pour l'équation des ondes $\partial_t^2 u - \Delta u = 0$, cet opérateur est **pseudo-différentiel** — son symbole, en coordonnées cartésiennes sur le demi-espace, vaut $\sqrt{s^2 + |\xi'|^2}$ et n'est pas polynomial. Son expression explicite dans l'espace physique requiert des techniques d'inversion fines (transformées de Bessel/Hankel, théorie des distributions, factorisation de Hadamard-Weierstrass, décomposition de Mittag-Leffler).

Le projet suit une démarche exploratoire : chaque géométrie impose une stratégie d'inversion différente, et le rapport retrace les impasses, reformulations et réussites de chaque étape.

---

## Structure du projet

### Chapitre 2 — DtN sur le demi-espace

Deux calculs indépendants du noyau de $\Lambda_0$ sur $\mathbb{R}^{n-1} \times \mathbb{R}^*_+$ :

- **Méthode 1** — Tables de Bessel–Hankel et partie finie de Hadamard : noyau causal en $(t^2 - |x'|^2)^{-3/2}$.
- **Méthode 2** — Laplacien au sens des distributions : parties finies de $r^{-3}$ et $r^{-2}$.

Le cas perturbé (potentiel *q(x)*) est également traité via l'équation intégrale de Lippmann-Schwinger, l'approximation de Born au premier ordre et la solution fondamentale retardée $E(x,t) = \delta(t-|x|)/(4\pi|x|)$.

### Chapitre 3 — DtN sur le disque unité

Géométrie bornée $\Omega = \{|x| < 1\} \subset \mathbb{R}^2$. Le symbole modal est

$$\sigma_n(s) = s \, \frac{I'_n(s)}{I_n(s)}$$

et admet des pôles aux zéros imaginaires $\pm i \, j_{n,k}$ des fonctions de Bessel modifiées. L'inversion directe terme à terme fait apparaître une série divergente de masses de Dirac. La résolution combine :

- **Factorisation de Hadamard-Weierstrass** de la dérivée logarithmique de $I_n$
- **Transfert de dérivée** ($s^2 \hat{f} = \mathcal{L}\{f''\}$) pour rendre la série absolument convergente
- Expression temporelle finale par convolutions à noyaux $\sin(j_{n,k} \, t)/j_{n,k}$

### Chapitre 4 — DtN sur le cylindre creux fini *(avec validation numérique)*

Cylindre $\Omega = S^1_R \times (0, L)$, deux bords $\Gamma_0$ et $\Gamma_L$. Le symbole devient **matriciel** :

$$
\widehat{\Lambda}_m(s) =
\begin{pmatrix}
\mu_m \coth(\mu_m L) & -\mu_m / \sinh(\mu_m L) \\
-\mu_m / \sinh(\mu_m L) & \mu_m \coth(\mu_m L)
\end{pmatrix}
$$

avec $\mu_m = \sqrt{s^2 + m^2/R^2}$.

L'inversion vers le domaine temporel combine :

1. **Décomposition de Mittag-Leffler** des entrées de la matrice
2. **Transfert de dérivée** pour rendre la série absolument convergente
3. Expression finale : convolutions temporelles à noyaux $\sin(\omega_{m,k} \, t)/\omega_{m,k}$, avec $\omega_{m,k}^2 = (k\pi/L)^2 + (m/R)^2$

La formule est validée numériquement par comparaison avec une solution de référence aux différences finies haute résolution (schéma centré d'ordre 2, $N_z = 1000$). L'accord est de l'ordre du pourcent pour les modes bas ($m \in \{0,1,2,3\}$), avec analyse détaillée de la dégradation aux grands modes (condensation des fréquences propres, amplification par le terme de masse, limite de la référence elle-même).

### Chapitre 5 — Problème inverse

Reconstruction des paramètres géométriques à partir de la seule connaissance de $\Lambda$ :

- **Disque** — Rayon *R* : méthodes par limite statique ou par fréquences propres.
- **Cylindre** — Longueur *L* : inversion par le coefficient diagonal, par le rapport des coefficients, ou par développement asymptotique haute fréquence.

---

## Contenu du dépôt

```
.
├── Rapport_PR_Elias_Massaro.pdf           # Rapport de recherche complet (6 chapitres)
├── validation_cylindre_v2.ipynb           # Notebook Jupyter — validation numérique (chapitre 4)
└── README.md
```

---

## Dépendances

```
numpy
matplotlib
jupyter
```

Installation :

```bash
pip install numpy matplotlib jupyter
```

---

## Lancer le notebook

```bash
jupyter notebook validation_cylindre_v2.ipynb
```

Le notebook est auto-contenu et couvre intégralement la validation du chapitre 4 : solution de référence par différences finies, évaluation de la formule spectrale, comparaison superposée pour les modes $m \in \{0, 1, 2, 3\}$, étude de convergence en $k_{\max}$, et analyse du régime haute fréquence ($m \in \{10, 40, 100\}$).
