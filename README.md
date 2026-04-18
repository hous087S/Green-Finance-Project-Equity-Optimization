# Equity Portfolio Optimisation with Net Zero Objectives

**Green Finance: Risk and Portfolio Management** — ENSAE Paris, Institut Polytechnique de Paris  
*Supervisor: Peter Tankov*

---

## Overview

This project solves a constrained equity portfolio optimisation problem under a **net zero decarbonisation pathway**, combining classical mean-variance theory with ESG constraints derived from real climate data.

The investment universe consists of **11 GICS sector synthetic assets**. Risk is modelled via **CAPM**, and the benchmark is a cap-weighted market proxy. The optimisation framework progressively layers climate constraints on top of a tracking-error minimisation objective.

---

## Problem Structure

### Question 1 — Benchmark Analysis
- Derive the **covariance matrix** under CAPM: $\Sigma = \sigma_m^2 \beta\beta^\top + \tilde{D}^2$
- Compute sector **volatilities**, **correlations**, and **implied risk premia**
- Evaluate benchmark **climate metrics**: carbon intensity CI(b), carbon momentum CM(b), green intensity GI(b)

### Question 2 — CTB Decarbonisation Pathway
- Minimise **tracking error volatility** subject to a Climate Transition Benchmark (CTB) constraint:

$$\text{CI}(w) \leq (1 - 30\%)(1 - 7\%)^t \cdot \text{CI}(b)$$

- Solved for $t \in \{0, 1, 2, 5, 10\}$ under both **Scope 1+2** and **Scope 1+2+3 upstream** emissions
- Derived **implied return bets** $\Delta\tilde{\mu}_i(w^\star)$ to interpret ESG constraints as implicit market views
- Analysed the **carbon drift** of the portfolio between rebalancing dates

### Question 3 — Additional Constraints
Three supplementary constraints are studied (individually and combined):

| Constraint | Purpose |
|---|---|
| $w_i \geq b_i / 2$ | Sector diversification floor |
| $\text{CM}(w) \leq \text{CM}^\star$ | Forward-looking decarbonisation tilt |
| $\text{GI}(w) \geq (1+G)\,\text{GI}(b)$ | EU Taxonomy green revenue alignment |

Key finding: the **green intensity** and **carbon intensity** constraints can conflict — Utilities has the highest green revenue share (8.4%) *and* the highest carbon intensity (1655 tCO₂e/\$mn), making some combined scenarios **infeasible**.

---

## Methods

- **Quadratic Programming** (QP) via `scipy.optimize` — tracking error minimisation with linear inequality constraints
- **Reverse optimisation** — recovering implied expected returns from the mean-variance FOC
- CAPM-based covariance structure, long-only constraints, full-investment requirement

---

## Repository

├── equity_opt_fin.ipynb      # Full implementation (Questions 1–3)
├── Equity_Optimization.pdf   # Mathematical report with derivations and results
└── problem_statement.pdf     # Original problem set

---

## Key Results at a Glance

| Scenario | TE vol | CI reduction | CM | GI |
|---|---|---|---|---|
| Baseline CTB ($t=0$) | 0.58% | 30.0% | −5.82% | 0.66% |
| + Sector floor $w_i \geq b_i/2$ | 0.80% | 30.0% | −5.87% | 0.70% |
| + Momentum CM⋆ = −6% | 0.79% | 30.0% | −6.00% | 0.68% |
| + Green intensity $G = 0.5$ | 5.92% | 30.0% | −6.50% | 1.26% |
| CTB at $t=10$ (Scope 1+2+3) | 8.17% | 66.1% | −0.68% | 0.10% |

---

## Stack

`Python` · `NumPy` · `Pandas` · `SciPy`

---

## Skills Demonstrated

Portfolio optimisation · ESG / Net Zero investing · CAPM · Quadratic programming · Reverse optimisation · Climate risk metrics (Scope 1/2/3, EU Taxonomy)
