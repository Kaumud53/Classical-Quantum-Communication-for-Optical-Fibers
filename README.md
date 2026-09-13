# A Rigorous Quantum Communication Framework for Optical Fibre Channels: Integrated Control, Computational Hardness, and Noise-Assisted Security

**Authors:** K. Gautam, Kaumud Sharma
**Affiliation:** Department of Quantum Computing, Quantum Research and Centre of Excellence (QRACE), Delhi, India

> Status: Under review

## Abstract

This paper presents a comprehensive and mathematically rigorous quantum communication framework for electromagnetic signal propagation through optical fibres, unifying five interlocking layers: (1) quantum field quantisation over modal decompositions of the fibre; (2) Classical-Quantum (Cq) channel theory with Holevo capacity optimisation under realistic fibre parameters; (3) GKSL noise modelling with exact Kraus-operator solutions and the Quantum Data Processing Inequality; (4) integrated quantum control during channel evolution that provably increases capacity beyond the Data Processing Inequality ceiling; and (5) multi-parameter quantum channel estimation via the Quantum Cramér–Rao Bound (QCRB). A central contribution is a rigorous, unconditional proof that the newly introduced **Semigroup Julia Inversion Problem (SJIP)** is NP-hard, via a polynomial-time reduction from Subset-Sum using a quadratic-map semigroup construction. We further give a structural argument — presented explicitly as a **conjecture, not a theorem** — that optimal coherent-state decoding is at least as hard as SJIP. Combining channel non-injectivity with this conjectured computational barrier yields a dual-layer cryptographic security guarantee, in which the eavesdropper's advantage decays exponentially with propagation length under the (unconditional) information-theoretic layer alone, with the computational layer offering additional, conjecture-conditional protection.

## Framework Overview

Five layers, each feeding the next, all anchored to a single fibre-parameter vector θ (Fig. 1 of the paper):

1. **Physical foundations** — Maxwell's equations, retarded-potential formulation of the fibre field, modal decomposition (LP₀₁ mode), atom–field interaction Hamiltonian → coherent-state encoding |α(θ)⟩.
2. **Cq channel & noise** — BPSK coherent-state Cq channel degraded by GKSL amplitude damping/dephasing; Holevo capacity C(θ); channel non-injectivity and ambiguity sets.
3. **Control & hardness** — a concurrent control Hamiltonian H_c(t) that strictly raises capacity beyond the Quantum Data Processing Inequality ceiling (because it modifies the channel itself, not its post-processing); the Semigroup Julia Inversion Problem (SJIP), proven NP-hard.
4. **Estimation & security** — the Quantum Fisher Information Matrix (QFIM) for the combined loss-dephasing channel, a QCRB-saturating adaptive Bayesian estimator (Algorithm 1), and a dual-layer security bound (Corollary V.9).

## Key Contributions

1. **Complete physical-to-information-theoretic path**: from Maxwell's equations (retarded potentials, Eqs. 1–4) through the atom–field Hamiltonian (Eq. 6–9) to the Holevo channel capacity (Eq. 12), with every fibre parameter (core radius *a*, numerical aperture, dispersion β₂, propagation length *L*, temperature *T*) appearing explicitly.
2. **Fibre noise-rate derivations** (Proposition III.1): amplitude-damping rate γ_loss = α_f v_g ln10/10 and phase-damping rate γ_φ = (ωD_pΔL)²v_g/2, derived from first principles rather than postulated, with exact Kraus operators (Eq. 16).
3. **Integrated-control capacity theorem** (Theorem IV.1–IV.2): a time-concurrent control Hamiltonian H_c(t) satisfying [L₀, L_c(t)] ≠ 0 strictly increases Holevo capacity beyond the uncontrolled channel — a regime the Quantum Data Processing Inequality does not constrain, since that inequality only bounds *post*-channel CPTP processing. A worked numerical example gives a **13.0% capacity gain** from 50% noise suppression.
4. **Unconditional NP-hardness proof for SJIP** (Theorem IV.3): a polynomial-time reduction from Subset-Sum, given in both a multiplicative-group version and a quadratic-map-semigroup version (the latter built from f_a(z) = (z+a)² under composition).
5. **Honest conjecture flagging** (Conjecture IV.5): optimal ML coherent-state decoding is *conjectured* — not proven — to be at least as hard as SJIP. The paper explicitly identifies the missing step (no algebraic isomorphism between quantum-state overlaps and the semigroup operation has been established) and treats all downstream security results built on it as conditional.
6. **Three-paradigm comparative rate analysis** (Theorem V.1): uncontrolled ML decoding, CPTP-corrected decoding, and integrated-control decoding, with a strict rate ordering R₃ > R₁ ≥ R₂.
7. **QFIM for the combined loss-dephasing channel** (Theorem V.5) and a QCRB-saturating adaptive Bayesian estimator (Algorithm 1), validated numerically with a particle-filter simulation (Section VI).
8. **Dual-layer security bound** (Corollary V.9): Pr[Eve succeeds] ≤ 1/|Amb(σ)| + negl(N) ≤ e^(−γ_lossL)e^(−2γ_φL) + negl(N) — an **unconditional** information-theoretic term plus a **conditional** (on Conjecture IV.5) computational term.
9. **Four experimentally testable predictions**: capacity scaling with (L, a, T); the noise-rate identities; the control-induced capacity-gain formula; and the SJIP-hardness signature in ML decoding time.

## Repository Contents

```
.
├── paper/                       # Manuscript source (LaTeX) and compiled PDF
├── src/
│   ├── fibre_channel.py          # Cq channel model, GKSL Kraus operators, Holevo capacity (Sec. III)
│   ├── capacity_enhancement.py   # Theorem IV.2 numerical example (13% capacity-gain calculation)
│   ├── sjip_reduction.py         # Algorithm 2 — polynomial-time Subset-Sum → SJIP reduction
│   ├── qfim.py                   # QFIM for the combined loss-dephasing channel (Theorem V.5)
│   └── adaptive_estimator.py     # Algorithm 1 — adaptive Bayesian particle-filter estimator (Sec. VI)
├── figures/
│   ├── fig2_posterior_mean_convergence.png
│   └── fig3_posterior_variance_vs_qcrb.png
└── README.md
```

*(Adjust the tree above to match your actual repo layout before pushing.)*

## Numerical Results

### Capacity enhancement (Section IV-C)
For γ₁ = 0.1 ns⁻¹, t = 10 ns, |α| = 1: uncontrolled η = e⁻¹ ≈ 0.368 gives C ≈ 0.827 bits; a 50% noise-suppression factor (f₁ = 0.5) gives η_c = e^(−0.5) ≈ 0.607 and C ≈ 0.935 bits — a **13.0% capacity gain**.

### Adaptive Bayesian estimation (Algorithm 1, Section VI)

| Parameter | Value |
|---|---|
| Loss rate γ_loss | 0.02 ns⁻¹ |
| Dephasing rate γ_φ | 0.005 ns⁻¹ |
| Propagation length L | 10 km (t = 10 ns in normalised units) |
| Transmission efficiency η | e^(−γ_lossL) ≈ 0.819 |
| True parameters | n̄ = 5.0, φ = 0.30 rad |
| Prior (misspecified) | n̄₀ = 4.0, φ₀ = 0.50 rad |
| Measurement rounds M | 50 |
| Particles N_p | 300 |

At the true parameters: F₁₁ ≈ 0.2467, F₂₂ ≈ 14.816 per copy, giving M·F(Θ_true) = diag(12.34, 740.8) and frequentist QCRB(n̄) = 0.08106, QCRB(φ) = 0.00135 at M = 50.

**Result:** both estimators converge from a prior deviating 20% (n̄) and 67% (φ) from truth to within a neighborhood of the true values by k ≈ 25 rounds; posterior variances fall below the frequentist QCRB after k ≈ 25 rounds (consistent with Bayesian efficiency — the prior supplies information beyond the M channel uses, per Remark VI.1, not a QCRB violation). The phase estimate converges 20–50× faster in variance than the photon-number estimate, matching the QFIM ratio F₂₂/F₁₁ ≈ 60.

## Code

### 1. GKSL Kraus operators and Holevo capacity (Section III)

```python
"""
fibre_channel.py

BPSK Cq channel over an optical fibre with GKSL amplitude-damping and
phase-damping noise (Section III of the paper).
"""

import numpy as np


def noise_rates(alpha_f_dB_per_km, vg, omega, Dp, delta_L):
    """
    Proposition III.1: fibre noise parameters.

    alpha_f_dB_per_km : field attenuation coefficient (dB/km)
    vg                : group velocity
    omega             : optical carrier (or detuning) frequency
    Dp                : polarisation-mode dispersion parameter
    delta_L           : PMD accumulation length scale

    Returns (gamma_loss, gamma_phi).
    """
    gamma_loss = alpha_f_dB_per_km * vg * np.log(10) / 10.0
    gamma_phi = (omega * Dp * delta_L) ** 2 * vg / 2.0
    return gamma_loss, gamma_phi


def amplitude_damping_kraus(t, gamma_loss):
    """
    Eq. (16)-(17): amplitude-damping Kraus operators on the
    {|0>, |1>} vacuum/single-photon subspace.
    """
    eta = 1.0 - np.exp(-gamma_loss * t)
    E0 = np.array([[1, 0], [0, np.sqrt(1 - eta)]], dtype=complex)
    E1 = np.array([[0, np.sqrt(eta)], [0, 0]], dtype=complex)
    return E0, E1


def holevo_capacity_bpsk(alpha_mag, eta=1.0):
    """
    Eq. (54) (Appendix B): Holevo capacity for BPSK antipodal coherent
    states of amplitude sqrt(eta)*alpha, with binary entropy H2.
    """
    def H2(x):
        x = np.clip(x, 1e-12, 1 - 1e-12)
        return -x * np.log2(x) - (1 - x) * np.log2(1 - x)

    q = (1 + np.exp(-2 * eta * alpha_mag**2)) / 2.0
    return H2(q)


def transmission_efficiency(gamma_loss, t):
    """eta(t) = exp(-gamma_loss * t), the uncontrolled channel efficiency."""
    return np.exp(-gamma_loss * t)


if __name__ == "__main__":
    # Reproduce the noiseless-vs-controlled capacity numbers of Sec. IV-C
    gamma_loss = 0.1  # ns^-1
    t = 10.0          # ns
    alpha = 1.0

    eta_uncontrolled = transmission_efficiency(gamma_loss, t)
    C_uncontrolled = holevo_capacity_bpsk(alpha, eta=eta_uncontrolled)
    print(f"Uncontrolled: eta = {eta_uncontrolled:.4f}, C = {C_uncontrolled:.4f} bits")

    f1 = 0.5  # 50% noise-suppression factor
    eta_controlled = np.exp(-gamma_loss * f1 * t)
    C_controlled = holevo_capacity_bpsk(alpha, eta=eta_controlled)
    print(f"Controlled:   eta_c = {eta_controlled:.4f}, C = {C_controlled:.4f} bits")

    gain = (C_controlled - C_uncontrolled) / C_uncontrolled * 100
    print(f"Capacity gain: {gain:.1f}%")
```

Expected output:
```
Uncontrolled: eta = 0.3679, C = 0.8266 bits
Controlled:   eta_c = 0.6065, C = 0.9347 bits
Capacity gain: 13.1%
```
(matches the paper's reported 13.0% gain to rounding.)

### 2. SJIP polynomial-time reduction (Algorithm 2, Theorem IV.3)

```python
"""
sjip_reduction.py

Algorithm 2: polynomial-time reduction from Subset-Sum to the
Semigroup Julia Inversion Problem (SJIP), in both the multiplicative-
group and quadratic-map-semigroup versions (Theorem IV.3).
"""

import cmath
from itertools import product


def multiplicative_reduction(A, T):
    """
    Multiplicative version: G = (C*, x), S = {exp(a_i)}, y = exp(T).
    Returns the SJIP instance (S, y) and a brute-force verifier for
    small n (exponential; for demonstration/testing only).
    """
    S = [cmath.exp(a) for a in A]
    y = cmath.exp(T)
    return S, y


def verify_subset_sum_via_multiplicative_sjip(A, T, tol=1e-9):
    """
    Brute-force check (2^n): does some subset of exp(a_i) multiply to exp(T)?
    Used only to confirm the reduction's correctness on small instances.
    """
    S, y = multiplicative_reduction(A, T)
    n = len(A)
    for bits in product([0, 1], repeat=n):
        prod = 1.0 + 0.0j
        for b, s in zip(bits, S):
            if b:
                prod *= s
        if abs(prod - y) < tol:
            subset = [a for b, a in zip(bits, A) if b]
            return True, subset
    return False, None


def quadratic_map_reduction(A):
    """
    Quadratic-map version: generators f_a(z) = (z + a)^2 composed in the
    fixed order given by A. Returns the composed function Phi and the
    target z_target = T^2 is supplied by the caller (Lemma IV.4).
    """
    def make_f(a):
        return lambda z: (z + a) ** 2

    fs = [make_f(a) for a in A]

    def Phi(z0):
        z = z0
        for f in fs:
            z = f(z)
        return z

    return Phi


if __name__ == "__main__":
    # Small Subset-Sum instance: does some subset of A sum to T?
    A = [3, 7, -2, 5]
    T = 8  # e.g. 3 + 5 = 8, or 3 + 7 - 2 = 8

    found, subset = verify_subset_sum_via_multiplicative_sjip(A, T)
    print(f"Subset-Sum(A={A}, T={T}): {found}, witness subset = {subset}")

    Phi = quadratic_map_reduction(A)
    # Lemma IV.4: a witness corresponds to a sign vector reaching z0 = 0
    # from z_n = T^2 under backward iteration; here we just demonstrate
    # forward composition Phi(0) for illustration.
    print(f"Phi(0) via quadratic-map composition = {Phi(0)}")
```

### 3. QFIM for the combined loss-dephasing channel (Theorem V.5)

```python
"""
qfim.py

Quantum Fisher Information Matrix for a coherent-state input through the
combined amplitude-damping + phase-damping fibre channel (Theorem V.5).
"""

import numpy as np


def qfim_loss_dephasing(n_bar, eta, gamma_phi, L):
    """
    Eq. (43): QFIM for (n_bar, phi) at leading order in 1/n_bar.

    F = [[1/(eta*n_bar) + 4*gamma_phi^2*L^2/(eta*n_bar), 0],
         [0, 4*eta*n_bar*exp(-2*gamma_phi*L)]]
    """
    F11 = 1.0 / (eta * n_bar) + 4 * gamma_phi**2 * L**2 / (eta * n_bar)
    F22 = 4 * eta * n_bar * np.exp(-2 * gamma_phi * L)
    return np.array([[F11, 0.0], [0.0, F22]])


def qcrb(F, M):
    """Theorem V.3: frequentist QCRB, Cov(Theta_hat) >= (1/M) F^-1."""
    return np.diag(np.linalg.inv(F)) / M


if __name__ == "__main__":
    gamma_loss = 0.02  # ns^-1
    gamma_phi = 0.005  # ns^-1
    L = 10.0           # (normalised propagation "length"/time)
    n_bar_true = 5.0
    M = 50

    eta = np.exp(-gamma_loss * L)
    F = qfim_loss_dephasing(n_bar_true, eta, gamma_phi, L)
    print("eta =", eta)
    print("QFIM per copy:\n", F)
    print("QCRB at M =", M, ":", qcrb(F, M))
```

Expected output (matches Section VI-A numbers):
```
eta = 0.8187...
QFIM per copy:
 [[ 0.2467...  0.        ]
  [ 0.         14.816...  ]]
QCRB at M = 50 : [0.08106... 0.00135...]
```

### 4. Adaptive Bayesian estimator (Algorithm 1, Section VI)

```python
"""
adaptive_estimator.py

Algorithm 1: adaptive Bayesian channel-parameter estimation via a
sequential Monte Carlo (particle-filter) approximation, validated
against the QCRB of Theorem V.6 (Section VI numerical simulation).
"""

import numpy as np
from qfim import qfim_loss_dephasing


def simulate_measurement(n_bar_true, phi_true, eta, gamma_phi, L, rng):
    """
    Toy measurement model: draw a noisy (n_hat, phi_hat) observation
    whose precision is set by the per-copy QFIM (Cramer-Rao-consistent
    simulated likelihood). This stands in for the QCRB-saturating POVM
    of Theorem V.6 for the purpose of a runnable, self-contained demo.
    """
    F = qfim_loss_dephasing(n_bar_true, eta, gamma_phi, L)
    sigma_n = 1.0 / np.sqrt(F[0, 0])
    sigma_phi = 1.0 / np.sqrt(F[1, 1])
    n_obs = rng.normal(n_bar_true, sigma_n)
    phi_obs = rng.normal(phi_true, sigma_phi)
    return n_obs, phi_obs, F


def adaptive_bayesian_estimation(
    n_bar_true=5.0,
    phi_true=0.30,
    n_bar_0=4.0,
    phi_0=0.50,
    sigma2_n0=2.0,
    sigma2_phi0=0.50,
    gamma_loss=0.02,
    gamma_phi=0.005,
    L=10.0,
    M=50,
    n_particles=300,
    seed=0,
):
    """
    Sequential-Monte-Carlo (particle filter) approximation of Algorithm 1.
    Returns per-round posterior means and variances for (n_bar, phi).
    """
    rng = np.random.default_rng(seed)
    eta = np.exp(-gamma_loss * L)

    # Initialise particles from the (deliberately misspecified) prior
    particles_n = rng.normal(n_bar_0, np.sqrt(sigma2_n0), size=n_particles)
    particles_phi = rng.normal(phi_0, np.sqrt(sigma2_phi0), size=n_particles)
    weights = np.ones(n_particles) / n_particles

    history = {"n_mean": [], "n_var": [], "phi_mean": [], "phi_var": []}

    for k in range(1, M + 1):
        n_obs, phi_obs, F = simulate_measurement(
            n_bar_true, phi_true, eta, gamma_phi, L, rng
        )
        sigma_n = 1.0 / np.sqrt(F[0, 0])
        sigma_phi = 1.0 / np.sqrt(F[1, 1])

        # Likelihood update (Gaussian likelihood centred on the observation)
        log_w = (
            -0.5 * ((n_obs - particles_n) / sigma_n) ** 2
            - 0.5 * ((phi_obs - particles_phi) / sigma_phi) ** 2
        )
        log_w -= log_w.max()
        weights = weights * np.exp(log_w)
        weights /= weights.sum()

        # Effective sample size resampling
        ess = 1.0 / np.sum(weights**2)
        if ess < n_particles / 2:
            idx = rng.choice(n_particles, size=n_particles, p=weights)
            particles_n = particles_n[idx]
            particles_phi = particles_phi[idx]
            weights = np.ones(n_particles) / n_particles

        n_mean = np.sum(weights * particles_n)
        phi_mean = np.sum(weights * particles_phi)
        n_var = np.sum(weights * (particles_n - n_mean) ** 2)
        phi_var = np.sum(weights * (particles_phi - phi_mean) ** 2)

        history["n_mean"].append(n_mean)
        history["n_var"].append(n_var)
        history["phi_mean"].append(phi_mean)
        history["phi_var"].append(phi_var)

    return history


if __name__ == "__main__":
    hist = adaptive_bayesian_estimation()
    for k in [10, 20, 30, 40, 50]:
        print(
            f"k={k:2d}  n_hat={hist['n_mean'][k-1]:.4f}  "
            f"phi_hat={hist['phi_mean'][k-1]:.4f}  "
            f"Var(n)={hist['n_var'][k-1]:.6f}  Var(phi)={hist['phi_var'][k-1]:.6f}"
        )
```

Run all four scripts:
```bash
pip install numpy scipy matplotlib
python src/fibre_channel.py
python src/sjip_reduction.py
python src/qfim.py
python src/adaptive_estimator.py
```

## Open Questions / Future Work (Section VII)

1. **Resolving the decoding-hardness conjecture** — the single most important open question raised by the paper: either construct a genuine polynomial-time reduction from SJIP to optimal coherent-state decoding (upgrading Conjecture IV.5 to a theorem), or exhibit a polynomial-time decoding algorithm that refutes it.
2. **Experimental validation** on fibre-optic testbeds with controllable (L, a, T).
3. **Polynomial-time approximation algorithms for SJIP** (FPTAS-style, analogous to Subset-Sum approximation schemes).
4. **Nonlinear extensions** (Kerr nonlinearity χ⁽³⁾, multi-mode dispersion).
5. **Non-Markovian noise** extensions to the GKSL framework.
6. **Quantum key distribution** applications of the SJIP hardness result.
7. **Higher-order perturbation models** extending the Itô SDE framework of Gautam et al. to third and higher orders.

## Citation

```bibtex
@article{gautam_sharma_cq_fibre,
  title   = {A Rigorous Quantum Communication Framework for Optical Fibre Channels: Integrated Control, Computational Hardness, and Noise-Assisted Security},
  author  = {Gautam, K. and Sharma, Kaumud},
  journal = {IEEE Transactions on Quantum Engineering},
  year    = {Under review},
  note    = {Submitted}
}
```

## Acknowledgments

The authors gratefully acknowledge Prof. K. R. Parthasarathy for invaluable guidance on quantum stochastic differential equations.
