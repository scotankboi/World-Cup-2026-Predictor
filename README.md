# 🏆 World Cup 2026 Advanced Match Predictor

A Bayesian hierarchical model and Monte Carlo simulation engine designed to predict the outcomes of the 2026 FIFA World Cup. 

Unlike standard machine learning classification models that simply output "Win/Loss/Draw", this project utilizes **probabilistic programming** to simulate the exact distribution of goals scored in a match, accounting for team strength, momentum, and statistical uncertainty.

---

## 🧠 Methodology & Mathematical Approach

This simulator avoids black-box machine learning in favor of an interpretable Bayesian framework. 

### 1. Feature Engineering
The model builds a global index for 286 international teams. Custom engineered features include:
* **Attacking Efficiency (AE):** Standardized historical goal-scoring metrics.
* **Score Sensitivity Index (SSI):** Measures how teams perform when trailing vs. leading.
* **Time-Decayed Weighting:** Recent matches are weighted higher using an exponential decay function (Half-life = 1095 days).

### 2. Bayesian Match Model (PyMC)
Match outcomes are modeled using a Negative Binomial distribution to account for overdispersion in football scores. The expected goals ($\lambda$) for a team are modeled as:

$$
\lambda_{\text{home}} = \exp(\text{intercept} + \text{home advantage} + \text{Attack}_{\text{home}} - \text{Defense}_{\text{away}})
$$

The model uses **Markov Chain Monte Carlo (MCMC) with a NUTS sampler** to estimate the posterior distributions for every team's attack and defense strength.

### 3. Monte Carlo Simulation Engine
Instead of predicting a single outcome, the engine runs **10,000 Monte Carlo simulations** of the entire tournament bracket. This generates precise probabilities for:
* Expected Points and Goal Differences in the Group Stage.
* Probabilities of advancing to the Round of 32, Quarter-Finals, and beyond.

---

## 🛠️ Tech Stack
* **Probabilistic Programming:** PyMC, ArviZ.
* **Data Processing & Math:** Pandas, NumPy, Scikit-Learn.
* **Simulation & Graph Theory:** NetworkX (for dynamic bracket generation and third-place advancements).

---
