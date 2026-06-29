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

## Conditional Distributions & Expectation

$$
\begin{align*}
\textbf{Discrete} & & & \textbf{Continous} \\
P_{X|Y}(x|y) &= P(X = x | Y = y) = \frac{P(X = x, Y = y)}{P(Y = y)} &  f_{X|Y}(x|y) &= \frac{f_{X,Y}(x,y)}{f_Y(y)} \\
\mathbb{E}[X|Y = y] &= \sum_x x P_{X|Y}(x|y) & \mathbb{E}[X|Y = y] &= \int_{-\infty}^{\infty} x f_{X|Y}(x|y) \, dx
\end{align*}
$$

**Important**: $\mathbb{E}[X|Y]$ is itself a random variable (function of $Y$)

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

#### Poisson Process

Models the number of events with $\{N(t) : t \geq 0\}$. It satisfies the following properties:

- **Independent Increments:** The number of events in non-overlapping intervals are independent.
- **Memoryless Property:** $\mathbb{P}(T_i > s + t \mid T_i > s) = \mathbb{P}(T_i > t)$.
- **Stationary Increments:** The number of events in an interval depends only on the length of the interval, not its starting point.
- **Rare Events:** The probability of more than one event in a very small interval is negligible.
- **Rate Parameter ($\lambda$):** Average number of events per unit time.
- **Counting Process:** $N(t)$ counts the number of events in the interval $[0, t]$.
- **Inter-arrival Times:** The time between consecutive events follows an **exponential distribution** with rate $\lambda$.

The number of events $N(t)$ in an interval of length $t$ follows a **Poisson distribution**:

$$
\mathbb{P}(N(t) = k) = \frac{(\lambda t)^k e^{-\lambda t}}{k!}, \quad k = 0, 1, 2, \dots
$$

For $N(t) \sim \text{Poisson}(\lambda t)$:
- **Mean:** $\mathbb{E}[N(t)] = \lambda t$
- **Variance:** $\text{Var}(N(t)) = \lambda t$

- **The time between consecutive events**, $T_i = S_i - S_{i-1}$ (where $S_i$ is the time of the $i$-th event), follows an **exponential distribution**: \
  $f_{T_i}(t) = \lambda e^{-\lambda t}, \quad t \geq 0$
- **Probability of $k$ Events in Time $t$**: \
  $\mathbb{P}(N(t) = k) = \frac{(\lambda t)^k e^{-\lambda t}}{k!}$
- **Probability of at Most $k$ Events in Time $t$**: \
  $\mathbb{P}(N(t) \leq k) = e^{-\lambda t} \sum_{i=0}^k \frac{(\lambda t)^i}{i!}$
- **Expected Time Until the $k$-th Event**: \
  $\mathbb{E}[S_k] = \frac{k}{\lambda}$
- **Probability of No Events in Time $t$**: \
  $\mathbb{P}(N(t) = 0) = e^{-\lambda t}$

### Transformation of Random Variables

For a continuous RV $X$ with density $f_X(x)$ and a **differentiable, strictly monotone** function $g$ for $y$ in the range of $g$; $f_Y(y) = 0$ outside:

$$
Y = g(X) \implies f_Y(y) = \frac{f_X(g^{-1}(y))}{|g'(g^{-1}(y))|}
$$

## Example: Joint Density of $X$ and $Y$

Joint density function: $f_{X,Y}(x,y) = \begin{cases} 10x^2 y, & \text{if } 0 \leq y \leq x \leq 1, \\ 0, & \text{otherwise} \end{cases}$

- **Marginal of $X$:** $f_X(x) = \int_0^x 10x^2 y \, dy = 5x^4, \quad \text{for } 0 \leq x \leq 1$
- **Marginal of $Y$:** $f_Y(y) = \int_y^1 10x^2 y \, dx = \frac{10y}{3}(1 - y^3), \quad \text{for } 0 \leq y \leq 1$
- **Independence Check:** $f_X(x) \cdot f_Y(y) = 5x^4 \cdot \frac{10y}{3}(1 - y^3) \neq 10x^2 y = f_{X,Y}(x,y)$
  _$X$ and $Y$ are not independent_
- **Distribution Function:** $F_X(x) = \int_0^x 5t^4 \, dt = x^5, \quad \text{for } 0 \leq x \leq 1$
- **Expectation:** $\mathbb{E}[X] = \int_0^1 x \cdot 5x^4 \, dx = 5 \int_0^1 x^5 \, dx = \boxed{\dfrac{5}{6}}$
- **Conditional Density:** $f_{Y|X}(y|x) = \dfrac{f_{X,Y}(x,y)}{f_X(x)} = \dfrac{10x^2 y}{5x^4} = \boxed{\dfrac{2y}{x^2}}, \quad \text{for } 0 \leq y \leq x$
- $\mathbb{P}(Y \leq X/2) = \int_0^1 \int_0^{x/2} 10x^2 y \, dy \, dx = \boxed{\dfrac{1}{4}}.$

## Example: Chebyshev’s Inequality for $S_{900}$

**Given:** $S_{900} \sim \text{Binomial}(n=900, p=1/3)$.
- $\mathbb{E}[S_{900}] = 300$
- $\text{Var}(S_{900}) = 900 \cdot \frac{1}{3} \cdot \frac{2}{3} = 200$

**Chebyshev’s Inequality:**
$$
\mathbb{P}(|S_{900} - 300| \leq 20) \geq 1 - \frac{\text{Var}(S_{900})}{20^2} = 1 - \frac{200}{400} = \frac{1}{2}.
$$

The probability is *greater than or equal to* $\frac{1}{2}$

## Example: Law of Large Numbers
By the **Weak Law of Large Numbers**, as $n \to \infty$:

$$
\frac{S_n}{n} \xrightarrow{\mathbb{P}} p = \frac{1}{3}.
$$

Precise statement:

$$
\lim_{n \to \infty} \mathbb{P}\left(\left|\frac{S_n}{n} - \frac{1}{3}\right| \geq \epsilon\right) = 0 \quad \forall \epsilon > 0.
$$

## Example: Central Limit Theorem Approximation

**Given:** $S \sim \text{Binomial}(n=160{,}000, p=0.5)$.
- $\mathbb{E}[S] = 80{,}000$
- $\text{Var}(S) = 40{,}000$
- $\sigma = 200$

**Approximation:**
$$
\mathbb{P}(S \leq 80{,}200) \approx \mathbb{P}\left(Z \leq \frac{80{,}200.5 - 80{,}000}{200}\right) = \mathbb{P}(Z \leq 1.0025) \approx \Phi(1) \approx \boxed{0.841}.
$$

## Example: Stochastic Process $Y_n = \frac{1}{2}(X_n + X_{n-1})$

**Given:** $X_n$ i.i.d., $\mathbb{E}[X_n] = 2$, $\text{Var}(X_n) = 3$

- **Moments of $Y_n$** \
  $\mathbb{E}[Y_n] = \frac{1}{2}(\mathbb{E}[X_n] + \mathbb{E}[X_{n-1}]) = \boxed{2}$ \
  $\text{Var}(Y_n) = \frac{1}{4}(\text{Var}(X_n) + \text{Var}(X_{n-1})) = \boxed{\dfrac{3}{2}}$ \
  $\mathbb{E}[Y_n^2] = \text{Var}(Y_n) + (\mathbb{E}[Y_n])^2 = \frac{3}{2} + 4 = \boxed{\dfrac{11}{2}}$
- **Correlation Function:** \
  **If** $X_m$ and $X_n$ **i.i.d.**: $R_X(m,n) = \mathbb{E}[X_m] \cdot \mathbb{E}[X_n] = \begin{cases} 7 = \mathbb{E}[X_n^2] & \text{if } m = n \\ 4 & \text{if } m \neq n \end{cases}$ \
  **else if** $X_m$ and $X_n$ **dependent**: $R_Y(m,n) = \mathbb{E}[Y_m Y_n] = \mathbb{E}\left[\left(\frac{X_m + X_{m-1}}{2}\right) \left(\frac{X_n + X_{n-1}}{2}\right)\right]= \begin{cases} \dfrac{11}{2}, & \text{if } m = n, \\ \dfrac{19}{4}, & \text{if } |m - n| = 1, \\ 4, & \text{if } |m - n| \geq 2. \end{cases}$ \
  _Expand the product_ inside the expectation \
  _Use linearity of expectation_ to split into sums of expectations \
  _Evaluate each term_ using:
   - $\mathbb{E}[X_i X_j]$ (from the correlation function of $X$)
   - $\mathbb{E}[X_i^2]$ (from the second moment of $X$)
- **Process Properties:** \
  Identically Distributed: Yes \
  Independent: No \
  Wide-Sense Stationary: Yes

## Example: Poisson Process (Rate $\lambda = 2$ per month)
- $\boldsymbol{\mathbb{P}(\text{at most 4 failures in first month})}$: \
  $N(1) \sim \text{Poisson}(2), \quad \mathbb{P}(N(1) \leq 4) = e^{-2} \sum_{k=0}^4 \frac{2^k}{k!} = \boxed{7e^{-2}}$
- $\boldsymbol{\mathbb{P}(\text{3 in first month AND 2 in next two months})}$: \
  $\mathbb{P}(N(1) = 3) = \frac{4}{3} e^{-2}, \quad \mathbb{P}(N(3) - N(1) = 2) \implies N(3) - N(1) \sim \text{Poisson}(\lambda \cdot \text{length}) = \text{Poisson}(2 \cdot 2) \implies 8 e^{-4}$ \
  _Joint probability:_ $\boxed{\dfrac{32}{3} e^{-6}}$
- $\boldsymbol{\mathbb{P}(\text{3 in first month} \mid \text{4 in first two months})}$: \
  $\mathbb{P}(N(1) = 3 \mid N(2) = 4) = \frac{\mathbb{P}(N(1) = 3 \text{ and } N(2) - N(1) = 1)}{\mathbb{P}(N(2) = 4)} = \boxed{\dfrac{1}{4}}$
- Expected Time Until 10th Failure: \
  For a Poisson process, the time of the $k$-th arrival is $\text{Gamma}(k, \lambda)$ \
  _Mean time:_ $\boxed{5 \text{ months}}$ (since $\mathbb{E}[T_{10}] = \frac{10}{\lambda} = 5$)
