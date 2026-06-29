---
title: Stochastic Modeling
author: ''
exports:
- format: pdf
  template: https://github.com/marbetschar/plain_latex_article/archive/refs/heads/main.zip
  output: StochMod-Cheatsheet.pdf
  id: stochmod-cheatsheet-pdf
downloads:
  - id: stochmod-cheatsheet-pdf
    title: Download as PDF
---

###  Common Mistakes
- **Independence vs. Uncorrelated**: Independent implies uncorrelated, but not vice versa (except for jointly normal RVs)
- **Continuous vs. Discrete**: Remember to use PMF for discrete and PDF for continuous RVs
- **Conditional Probability**: Always check that $P(F) > 0$ before using $P(E|F)$
- **Expectation of Functions**: $\mathbb{E}[g(X)] \neq g(\mathbb{E}[X])$ in general (Jensen's inequality)
- **Variance of Sums**: $\operatorname{Var}(X+Y) = \operatorname{Var}(X) + \operatorname{Var}(Y) + 2\operatorname{Cov}(X,Y)$
- **Markov Chain Convergence**: Requires **both** irreducibility **and** aperiodicity

### Problem-Solving Strategies

1. **Identify the Distribution**: Recognize which distribution the problem involves
2. **Use Definitions**: Start with the definition (PMF, PDF, or property)
3. **Check Conditions**: Verify all conditions are met before applying theorems
4. **Use Linearity**: Expectation is linear - use this whenever possible
5. **Conditioning**: Break complex problems into simpler conditional problems
6. **Symmetry**: Look for symmetry to simplify calculations
7. **Approximations**: Use CLT for large $n$ approximations

### Differentiation Rules

|  |  |
|------|---------|
| **Power Rule** | $\frac{d}{dx} x^n = n x^{n-1}$ |
| **Exponential** | $\frac{d}{dx} e^{ax} = a e^{ax}$ |
| **Natural Log** | $\frac{d}{dx} \ln(x) = \frac{1}{x}$ |
| **Product Rule** | $\frac{d}{dx} [f(x)g(x)] = f'(x)g(x) + f(x)g'(x)$ |
| **Quotient Rule** | $\frac{d}{dx} \left[\frac{f(x)}{g(x)}\right] = \frac{f'(x)g(x) - f(x)g'(x)}{[g(x)]^2}$ |
| **Chain Rule** | $\frac{d}{dx} f(g(x)) = f'(g(x)) \cdot g'(x)$ |

### Integration Rules

|  |                                                                   |
|------|-------------------------------------------------------------------|
| **Power Rule** | $\int x^n dx = \frac{x^{n+1}}{n+1} + C$ (for $n \neq -1$)         |
| **Exponential** | $\int e^{ax} dx = \frac{1}{a} e^{ax} + C$                         |
| **Natural Log** | $\int \frac{1}{x} dx = \ln\|x                             \| + C$ |
| **Integration by Parts** | $\int u dv = uv - \int v du$                                      |

$$
\begin{align*}
\int x e^{ax} \, dx &= uv - \int v \, du \\
u &= x & dv &= e^{ax} \, dx \\
du &= dx & v &= \frac{e^{ax}}{a}
\end{align*}
$$

$$
\begin{align*}
\int_{-\infty}^{\infty} e^{-x^2} dx &= \sqrt{\pi} &
\int_0^{\infty} e^{-ax} dx &= \frac{1}{a} \quad \text{for } a > 0 \\
\int_0^{\infty} x e^{-ax} dx &= \frac{1}{a^2}  &
\int_0^{\infty} x^2 e^{-ax} dx &= \frac{2}{a^3}
\end{align*}
$$

### Probability

$$
\begin{align*}
P(E|F) &= \frac{P(E \cap F)}{P(F)} & P(E) &= P(E|A)P(A) + P(E|A^c)P(A^c) \\
P(A|E) &= \frac{P(E|A)P(A)}{P(E)} & P(A \cap B) &= P(A)P(B|A) = P(B)P(A|B)
\end{align*}
$$

### Law of Total Probability

- $P(E) = \sum_{i=1}^n P(E|A_i) \cdot P(A_i)$
- Simplified (for binary partition): $P(E) = P(E|A) \cdot P(A) + P(E|A^c) \cdot P(A^c)$

### Bayes' Theorem

$$
P(A|E) = \frac{P(E|A) \cdot P(A)}{P(E)} = \frac{P(E|A) \cdot P(A)}{P(E|A) \cdot P(A) + P(E|A^c) \cdot P(A^c)}
$$

### Expectation, Variance, Covariance, Correlation Coefficient (normalized Covariance)

$$
\begin{align*}
\boldsymbol{\mathbb{E}[X]} &= \sum x P(X=x) & \boldsymbol{\mathbb{E}[X]} &= \int x f_X(x) dx \\
\boldsymbol{\operatorname{Var}(X)} &= \mathbb{E}[X^2] - (\mathbb{E}[X])^2 & \boldsymbol{\operatorname{Var}(aX+b)} &= a^2 \operatorname{Var}(X) \\
\boldsymbol{\operatorname{Cov}(X,Y)} &= \mathbb{E}[XY] - \mathbb{E}[X]\mathbb{E}[Y] & \boldsymbol{\rho_{X,Y}} &= \frac{\operatorname{Cov}(X,Y)}{\sqrt{\operatorname{Var}(X)\operatorname{Var}(Y)}} \in [-1, 1]
\end{align*}
$$

$$
\mathbb{E}[aX + bY] = a\mathbb{E}[X] + b\mathbb{E}[Y] \quad \text{for any RVs } X, Y \text{ and constants } a, b
$$

$$
\begin{align*}
\operatorname{Var}(aX) &= a^2 \operatorname{Var}(X) \\
\operatorname{Var}(X + Y) &= \operatorname{Var}(X) + \operatorname{Var}(Y) + 2\operatorname{Cov}(X, Y) \\
\operatorname{Var}(X + c) &= \operatorname{Var}(X) \quad \text{for constant } c
\end{align*}
$$

$$
\begin{align*}
\operatorname{Cov}(X,X) &= \operatorname{Var}(X) \\
\operatorname{Cov}(X,Y) &= \operatorname{Cov}(Y,X) \\
\operatorname{Cov}(aX + b, cY + d) &= ac \operatorname{Cov}(X,Y) \\
\operatorname{Cov}(X + Y, Z) &= \operatorname{Cov}(X,Z) + \operatorname{Cov}(Y,Z) \\
\operatorname{Cov}(X, Y + Z) &= \operatorname{Cov}(X,Y) + \operatorname{Cov}(X,Z)
\end{align*}
$$

### Law of Total Expectation

$$
\mathbb{E}[X] = \mathbb{E}[\mathbb{E}[X|Y]]
$$

- Discrete $Y$: $\mathbb{E}[X] = \sum_y \mathbb{E}[X|Y = y] P(Y = y)$
- Continuous $Y$: $\mathbb{E}[X] = \int_{-\infty}^{\infty} \mathbb{E}[X|Y = y] f_Y(y) \, dy$

### Conditional Variance

$$
\operatorname{Var}(X|Y = y) = \mathbb{E}[X^2|Y = y] - (\mathbb{E}[X|Y = y])^2
$$

**Law of Total Variance**

$$
\operatorname{Var}(X) = \mathbb{E}[\operatorname{Var}(X|Y)] + \operatorname{Var}(\mathbb{E}[X|Y])
$$

### Distributions

|                                     | **PMF  $P(X=k)$**                     | **Support** | $\boldsymbol{\mathbb{E}[X]}$ | $\boldsymbol{\operatorname{Var}(X)}$ | **MGF** |
|-------------------------------------|-------------------------------------|---------|------------------------------|----------------------------------|-----|
| **Uniform** $(a, b), n = b - a + 1$ | $\frac{1}{n}$                       | $k \in \{1,\dots,n\}$ | $\frac{a+b}{2}$              | $\frac{n^2-1}{12}$               | $\frac{e^{at} - e^{(b+1)t}}{n(1 - e^t)}$ |
| **Bernoulli** $(p)$                 | $p^k(1-p)^{1-k}$                    | $k \in \{0,1\}$ | $p$                          | $p(1-p)$                         | $pe^t + (1-p)$ |
| **Binomial** $(n, p)$               | $\binom{n}{k}p^k(1-p)^{n-k}$        | $k \in \{0,\dots,n\}$ | $np$                         | $np(1-p)$                        | $(pe^t + 1-p)^n$ |
| **Geometric** $(p)$                 | $(1-p)^{k-1}p$                      | $k \in \mathbb{N}$ | $\frac{1}{p}$                | $\frac{1-p}{p^2}$                | $\frac{pe^t}{1-(1-p)e^t}$ |
| **Poisson** $(\lambda)$             | $\frac{\lambda^k e^{-\lambda}}{k!}$ | $k \in \mathbb{N}_0$ | $\lambda$                    | $\lambda$                        | $e^{\lambda(e^t-1)}$ |

|                              | **PDF $f(x)$**                                                           | **Support** | $\boldsymbol{\mathbb{E}[X]}$ | $\boldsymbol{\operatorname{Var}(X)}$ | **MGF** |
|------------------------------|----------------------------------------------------------------------|---------|------------------------------|--------------------------------------|-----|
| **Uniform** $(a, b)$         | $\frac{1}{b-a}$                                                      | $x \in [a,b]$ | $\frac{a+b}{2}$              | $\frac{(b-a)^2}{12}$                 | $\begin{cases}\frac{e^{tb} - e^{ta}}{t(b-a)} & \text{for } t \neq 0 \\ 1 & \text{for } t = 0 \end{cases}$ |
| **Exponential** $(\lambda)$  | $\lambda e^{-\lambda x}$                                      | $x \geq 0$ | $\frac{1}{\lambda}$          | $\frac{1}{\lambda^2}$                | $\frac{\lambda}{\lambda - t}$ |
| **Normal** $(\mu, \sigma^2)$ | $\frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{(x-\mu)^2}{2\sigma^2}}$ | $x \in \mathbb{R}$ | $\mu$                        | $\sigma^2$                           | $e^{t\mu + \frac{1}{2}t^2\sigma^2}$ |

**Normal Distribution**

- **Standard Normal**: $Z \sim N(0,1)$ with standard normal CDF $F_X(z) = \Phi(z) = \frac{1}{\sqrt{2\pi}} \int_{-\infty}^z e^{-t^2/2} \, dt$
- **Standardization**: If $X \sim N(\mu, \sigma^2)$, then $Z = \frac{X - \mu}{\sigma} \sim N(0,1)$
- **Probability Calculation**: $P(X \leq t) = \Phi\left(\frac{t - \mu}{\sigma}\right)$
- **Symmetric Properties**: $\Phi(-z) = 1 - \Phi(z) \quad \text{and} \quad \Phi(0) = 0.5$

## Joint Distributions

- **Joint Distribution**: $F_{X,Y}(x,y) = P(X \leq x, Y \leq y)$
- **Marginal Distribution**: $F_X(x) = \lim_{y\to\infty} F_{X,Y}(x,y)$
- **Joint PMF**: $p_{X,Y}(x,y) = P(X = x, Y = y)$, **Joint PDF**: $f_{X,Y}(x,y)$
- **Marginal PDF**: $f_X(x) = \int_{-\infty}^{\infty} f_{X,Y}(x,y) \, dy$

### Independence of Random Variables

$X$ and $Y$ are independent if one of the following is true:

$$
\begin{aligned}
F_{X,Y}(a,b) &= F_X(a) F_Y(b) \quad \forall a,b \\
f_{X,Y}(x,y) &= f_X(x)f_Y(y) \quad \text{, (continous RV)} \\
P(X=x, Y=y) &= P(X=x)P(Y=y) \quad \text{, (discrete RV)}
\end{aligned}
$$

**Consequences of Independence**

$$
\begin{align*}
\mathbb{E}[XY] &= \mathbb{E}[X]\mathbb{E}[Y] \\
\operatorname{Cov}(X,Y) &= 0 \\
\operatorname{Var}(X+Y) &= \operatorname{Var}(X) + \operatorname{Var}(Y) \\
\phi_{X+Y}(t) &= \phi_X(t) \phi_Y(t)
\end{align*}
$$

### Limit Theorems

$$
\begin{align*}
\textbf{LLN: } \frac{S_n}{n} &\xrightarrow{P} \mu & \textbf{CLT: } Z = \frac{S_n - \mu}{\sigma} &\xrightarrow{d} N(0,1) \\
\textbf{Chebyshev: } P(|X-\mu| \geq \varepsilon) &\leq \frac{\sigma^2}{\varepsilon^2} & \textbf{Markov: } P(X \geq a) &\leq \frac{\mathbb{E}[X]}{a}
\end{align*}
$$

### Markov Chains

$$
\begin{align*}
\textbf{Markov: } P(X_{n+1}|X_n, \ldots, X_0) &= P(X_{n+1}|X_n) & \textbf{Chapman-Kolmogorov: } p_{ij}^{(m+n)} &= \sum_k p_{ik}^{(m)} p_{kj}^{(n)} \\
\textbf{Stationary: } \vec{\pi} &= \vec{\pi} P & \textbf{Convergence: } \vec{\nu} P^n &\to \vec{\pi}
\end{align*}
$$

### Stochastic Processes

$$
\begin{align*}
\textbf{Mean: } m_X(t) &= \mathbb{E}[X_t] &
\textbf{Variance: } \text{Var}(X_t) &= \mathbb{E}[X_t^2] - (\mathbb{E}[X_t])^2 \\
\textbf{Covariance: } C_X(t_1,t_2) &= R_X(t_1,t_2) - m_X(t_1)m_X(t_2) &
\textbf{Correlation: } R_X(t_1, t_2) &= \mathbb{E}[X_{t_1} X_{t_2}]
\end{align*}
$$

_zero-mean processes:_ $R_X(t_1, t_2) = \operatorname{Cov}(X_{t_1}, X_{t_2})$

|  | **Description**               | $\boldsymbol{m_X(t)}$  | $\boldsymbol{Var(X_t)}$ | $\boldsymbol{R_X(t_1, t_2)}$ |
|---------|-----------------------------|------------------|-------------------------|-------------|
| **Bernoulli** | $X_n$ i.i.d. $\pm 1$ valued | $2p-1$           | $4p(1-p)$               | $(2p-1)^2$ for $t_1\neq t_2$ |
| **Random Walk** | $X_n = \sum_{i=1}^n B_i$    | $0$ (if $p=1/2$) | $n$                     | $\min(t_1, t_2)$ |
| **Brownian Motion** | Continuous limit of RW      | $0$              | $t$                     | $\min(t_1, t_2)$ |
| **Poisson** | Counts events in time       | $\lambda t$      | $\lambda t$             | $\lambda \min(t_1, t_2)$ |
| **White Noise**        | $X_t \sim \text{i.i.d.}(0, \sigma^2)$ | |                         | $\sigma^2 \delta_{t_1,t_2}$ for $\delta_{t_1,t_2}$ := if ($t_1 = t_2$) 1 else 0 |
| **Wiener Process**     | $W_t \sim \mathcal{N}(0, t)$          | |                         | $\min(t_1, t_2)$                                                       |

**Wide-Sense Stationary (WSS)**:
- Constant mean: $m_X(t) = m$ for all $t$
- Correlation depends only on time difference: $R_X(t_1, t_2) = R_X(|t_2 - t_1|)$

### Transformation of Random Variables

For a continuous RV $X$ with density $f_X(x)$ and a **differentiable, strictly monotone** function $g$ for $y$ in the range of $g$; $f_Y(y) = 0$ outside:

$$
Y = g(X) \implies f_Y(y) = \frac{f_X(g^{-1}(y))}{|g'(g^{-1}(y))|}
$$
