# STATS 102B — Final Project: Bootstrap Confidence Intervals & Gradient Descent Algorithms

Comprehensive project covering two main topics:
1. **Bootstrap simulation** for confidence interval evaluation of Weibull-distributed data.  
2. **Gradient descent algorithms** (standard, Polyak’s Heavy Ball, Nesterov’s Momentum, and Stochastic GD) applied to high-dimensional regression.  

---

## Section 1 — Bootstrap Simulation (Problem 1)

### Objective
Evaluate convergence probability and average CI length for four types of 95% bootstrap intervals:
- **Normal**, **Basic**, **Percentile**, and **Studentized**.

### Simulation setup
- Distribution: Weibull(k = 1.5, λ = 1)  
- True median = λ × (log 2)^(1/k)  
- True standard deviation = √[λ² × (Γ(1 + 2/k) − Γ²(1 + 1/k))]  
- Sample sizes n = 100, 250  
- Simulations M = 100, 500  
- Bootstrap replicates B = 5000  
- Confidence level = 95%  
- Coverage = proportion of intervals containing the true value.  
- Average length = mean CI width.  

### Key findings
- Coverage probabilities increase with sample size (n = 250 > 100).  
- Percentile CIs provided slightly higher coverage at modest n.  
- All methods had similar interval lengths.  
- Larger n → shorter intervals (more precise estimates).  
- Studentized and Normal CIs performed best for smaller n; Basic CI slightly better for large n.  

---

## Section 2 — Gradient Descent Algorithms (Problem 2)

### Dataset generation
- n = 100,000, p = 20 predictors, all true β = 3.  
- Predictors X ∼ N(0, Σ), with ρ = 0.99 (first p/2) and 0.9 (second p/2).  
- Errors ε ∼ N(0, 1.25²).  
- Response: y = Xβ + ε.  

### Implemented methods
- **Standard Gradient Descent** — step = 0.01, tolerance = 1e-6; converged ≈ 15,500 iterations.  
- **Polyak’s Heavy Ball** — γ = 0.9; converged ≈ 2,673 iterations.  
- **Nesterov’s Momentum** — γ = 0.9; converged ≈ 2,677 iterations.  
- **Stochastic GD (mini-batch = 2000)** — both momentum variants; 30,000 iterations (no full convergence).  

### Results summary
- All estimated β ≈ 3 with minimal deviation (< 0.05).  
- Momentum methods dramatically improved convergence speed (≈ 6× faster).  
- Stochastic GD maintained accuracy with faster iteration throughput, ideal for large datasets.  
- OLS benchmark: identical coefficients (Adjusted R² = 0.9995).  

---