# Problem 1
 # Exploring the Central Limit Theorem through Simulations

---

##  Motivation

The **Central Limit Theorem (CLT)** is one of the most important concepts in statistics. It states that:

> **If you take sufficiently large random samples from any population (with finite mean and variance), the distribution of the sample means will tend toward a normal distribution.**

Mathematically:

Let \( X_1, X_2, \dots, X_n \) be i.i.d. random variables from a population with mean \( \mu \) and variance \( \sigma^2 \). Then the sample mean:

$$
\bar{X}_n = \frac{1}{n} \sum_{i=1}^{n} X_i
$$

Will follow approximately:

$$
\bar{X}_n \sim \mathcal{N}\left( \mu, \frac{\sigma^2}{n} \right)
$$

as \( n \to \infty \), regardless of the original distribution of \( X \).

Simulating this process offers a **powerful and intuitive demonstration** of how and why the CLT works.

---

## Task Overview

### 1. Simulate populations from:
- Uniform distribution
- Exponential distribution
- Binomial distribution

### 2. For each:
- Sample means with \( n = 5, 10, 30, 50 \)
- Repeat sampling 5,000 times
- Plot histograms of sample means

### 3. Explore:
- Shape convergence to normal
- Effect of original variance
- Application in real-world contexts

---

##  Python Code: CLT Simulation Engine

```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

def clt_simulation(population_func, sample_sizes, n_trials=5000, pop_size=100000, title=""):
    """
    Simulates the Central Limit Theorem:
    - population_func: function that returns a sample of size pop_size
    - sample_sizes: list of sample sizes (e.g., [5, 10, 30, 50])
    - n_trials: how many sample means to compute per sample size
    - title: title to use in plots
    """
    population = population_func(pop_size)
    true_mean = np.mean(population)
    true_std = np.std(population)

    print(f"Population Mean: {true_mean:.2f}, Std Dev: {true_std:.2f}")

    fig, axes = plt.subplots(1, len(sample_sizes), figsize=(18, 4))
    for i, n in enumerate(sample_sizes):
        sample_means = [np.mean(np.random.choice(population, size=n)) for _ in range(n_trials)]
        sns.histplot(sample_means, kde=True, ax=axes[i], color="skyblue", stat="density")
        axes[i].set_title(f"n = {n}")
        axes[i].axvline(true_mean, color='red', linestyle='--', label='True Mean')
        axes[i].legend()
        axes[i].set_xlabel("Sample Mean")
        axes[i].set_ylabel("Density")

    fig.suptitle(f"CLT Simulation: {title}", fontsize=16)
    plt.tight_layout()
    plt.show()
```
