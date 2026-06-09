---
title: Stochastic Modeling
authors:
  - name: Erich Baur
    affiliation: ZHAW School of Engineering
exports:
- format: pdf
  template: https://github.com/marbetschar/plain_latex_article/archive/refs/heads/main.zip
  output: Stochastic-Modeling.pdf
  id: stochastic-modeling-pdf
downloads:
  - id: stochastic-modeling-pdf
    title: Download as PDF
---

# Stochastic Modeling

## Probability Theory Fundamentals

### Probability Space & Axioms

A probability space is a triple $(\Omega, \mathcal{A}, P)$ where:

- **$\Omega$**: Sample space - set of all possible outcomes
- **$\mathcal{A}$**: $\sigma$-algebra - set of all measurable events (subsets of $\Omega$)
- **$P$**: Probability measure satisfying **Kolmogorov's Axioms**:

```{math}
\begin{align*}
1. &\quad 0 \leq P(E) \leq 1 \quad \forall E \in \mathcal{A} \\
2. &\quad P(\Omega) = 1 \\
3. &\quad P\left(\bigcup_{i=1}^{\infty} E_i\right) = \sum_{i=1}^{\infty} P(E_i) \quad \text{for pairwise disjoint } E_i
\end{align*}
```

### Key Properties

```{math}
\begin{align*}
P(\emptyset) &= 0 \\
P(A^c) &= 1 - P(A) \\
P(A \setminus B) &= P(A) - P(A \cap B) \\
P(A \cup B) &= P(A) + P(B) - P(A \cap B) \quad \text{(Inclusion-Exclusion)}
\end{align*}
```

### Conditional Probability

```{definition} Conditional Probability
The probability of event $E$ given that $F$ has occurred:
\begin{equation*}
P(E|F) = \frac{P(E \cap F)}{P(F)} \quad \text{for } P(F) > 0
\end{equation*}
```

**Interpretation**: Restricts the sample space to $F$ and considers the relative frequency of $E$ within $F$.

### Independence

```{definition} Independent Events
Two events $E, F$ are **independent** if:
\begin{equation*}
P(E \cap F) = P(E) \cdot P(F)
\end{equation*}
Equivalently: $P(E|F) = P(E)$ or $P(F|E) = P(F)$.
```

For $n$ events $E_1, E_2, \ldots, E_n$:
```{math}
P\left(\bigcap_{i=1}^n E_i\right) = \prod_{i=1}^n P(E_i)
```

**Important**: Independence is pairwise and for all subsets, not just pairs.

### Law of Total Probability

For a partition $A_1, A_2, \ldots, A_n$ of $\Omega$:
```{math}
P(E) = \sum_{i=1}^n P(E|A_i) \cdot P(A_i)
```

Simplified (for binary partition):
```{math}
P(E) = P(E|A) \cdot P(A) + P(E|A^c) \cdot P(A^c)
```

### Bayes' Theorem

```{math}
P(A|E) = \frac{P(E|A) \cdot P(A)}{P(E)} = \frac{P(E|A) \cdot P(A)}{P(E|A) \cdot P(A) + P(E|A^c) \cdot P(A^c)}
```

**Example**: Medical testing - given test result, compute probability of disease.

---

## Random Variables

### Definition

A **random variable (RV)** $X: \Omega \to \mathbb{R}$ assigns a numerical value to each outcome.

### Types of Random Variables

| Type | Definition | Example |
|------|------------|---------|
| Discrete | Takes finite or countable values | Dice roll, coin toss |
| Continuous | Takes uncountable values | Height, time |

### Probability Mass Function (PMF)

For discrete RV $X$:
```{math}
P(X = x_i) = p_X(x_i) \quad \text{where } \sum_i p_X(x_i) = 1
```

### Probability Density Function (PDF)

For continuous RV $X$:
```{math}
P(a \leq X \leq b) = \int_a^b f_X(x) \, dx \quad \text{where } \int_{-\infty}^{\infty} f_X(x) \, dx = 1
```

### Distribution Function (CDF)

For any RV $X$:
```{math}
F_X(t) = P(X \leq t) = \begin{cases}
\sum_{x_i \leq t} P(X = x_i) & \text{for discrete } X \\
\int_{-\infty}^t f_X(x) \, dx & \text{for continuous } X
\end{cases}
```

**Properties**: $F_X$ is right-continuous, non-decreasing, with $\lim_{t\to-\infty} F_X(t) = 0$ and $\lim_{t\to\infty} F_X(t) = 1$.

### Expectation (Mean)

```{math}
\mathbb{E}[X] = \begin{cases}
\sum_i x_i P(X = x_i) & \text{for discrete } X \\
\int_{-\infty}^{\infty} x f_X(x) \, dx & \text{for continuous } X
\end{cases}
```

**Linearity of Expectation**:
```{math}
\mathbb{E}[aX + bY] = a\mathbb{E}[X] + b\mathbb{E}[Y] \quad \text{for any RVs } X, Y \text{ and constants } a, b
```

**Important**: Linearity holds **regardless of independence**.

### Variance

```{math}
\operatorname{Var}(X) = \mathbb{E}[(X - \mathbb{E}[X])^2] = \mathbb{E}[X^2] - (\mathbb{E}[X])^2
```

**Properties**:
```{math}
\begin{align*}
\operatorname{Var}(aX) &= a^2 \operatorname{Var}(X) \\
\operatorname{Var}(X + Y) &= \operatorname{Var}(X) + \operatorname{Var}(Y) + 2\operatorname{Cov}(X, Y) \\
\operatorname{Var}(X + c) &= \operatorname{Var}(X) \quad \text{for constant } c
\end{align*}
```

### Moment Generating Function (MGF)

```{math}
\phi_X(t) = \mathbb{E}[e^{tX}] = \begin{cases}
\sum_i e^{t x_i} P(X = x_i) & \text{for discrete } X \\
\int_{-\infty}^{\infty} e^{t x} f_X(x) \, dx & \text{for continuous } X
\end{cases}
```

**Important Property**: The $n$-th derivative at $t=0$ gives the $n$-th moment:
```{math}
\phi_X^{(n)}(0) = \mathbb{E}[X^n]
```

**Taylor Expansion**:
```{math}
\phi_X(t) = \sum_{n=0}^{\infty} \frac{t^n}{n!} \mathbb{E}[X^n]
```

---

## Important Discrete Distributions

```{table} Common Discrete Distributions
| Distribution | PMF | Support | $\mathbb{E}[X]$ | $\operatorname{Var}(X)$ | MGF |
|--------------|-----|---------|--------|---------------|-----|
| **Uniform** | $P(X=k) = \frac{1}{n}$ | $k \in \{1,2,\ldots,n\}$ | $\frac{n+1}{2}$ | $\frac{n^2-1}{12}$ | $\frac{e^t(1-e^{nt})}{n(1-e^t)}$ |
| **Bernoulli** | $P(X=k) = p^k(1-p)^{1-k}$ | $k \in \{0,1\}$ | $p$ | $p(1-p)$ | $pe^t + (1-p)$ |
| **Binomial** | $P(X=k) = \binom{n}{k}p^k(1-p)^{n-k}$ | $k \in \{0,1,\ldots,n\}$ | $np$ | $np(1-p)$ | $(pe^t + 1-p)^n$ |
| **Geometric** | $P(X=k) = (1-p)^{k-1}p$ | $k \in \mathbb{N}$ | $\frac{1}{p}$ | $\frac{1-p}{p^2}$ | $\frac{pe^t}{1-(1-p)e^t}$ |
| **Poisson** | $P(X=k) = \frac{\lambda^k e^{-\lambda}}{k!}$ | $k \in \mathbb{N}_0$ | $\lambda$ | $\lambda$ | $e^{\lambda(e^t-1)}$ |
```

### Bernoulli Distribution

Models a single yes/no experiment with success probability $p$.

**Example**: Coin toss, single trial in an experiment.

### Binomial Distribution

Models the number of successes in $n$ independent Bernoulli trials.

### Geometric Distribution

Models the number of trials until the first success.

```{admonition} Memoryless Property
:class: important
For $X \sim \text{Geom}(p)$:
\begin{equation*}
P(X > k + l | X > k) = P(X > l) \quad \forall k, l \geq 0
\end{equation*}
This means the distribution "forgets" how long it has been waiting.
```

**Example**: Number of coin tosses until the first head appears.

### Coupon Collector's Problem

**Problem**: How many boxes must you buy to collect all $n$ different coupons?

**Solution**: Let $S_n = X_1 + X_2 + \ldots + X_n$ where $X_k \sim \text{Geom}\left(\frac{n-(k-1)}{n}\right)$.

```{math}
\mathbb{E}[S_n] = n \sum_{k=1}^n \frac{1}{k} = n H_n \approx n \ln(n) + \gamma n
```

where $H_n = \sum_{k=1}^n \frac{1}{k}$ is the $n$-th harmonic number and $\gamma \approx 0.5772$ is the Euler-Mascheroni constant.

---

## Important Continuous Distributions

```{table} Common Continuous Distributions
| Distribution | PDF | Support | $\mathbb{E}[X]$ | $\operatorname{Var}(X)$ | MGF |
|--------------|-----|---------|--------|---------------|-----|
| **Uniform** | $f(x) = \frac{1}{b-a}$ | $x \in [a,b]$ | $\frac{a+b}{2}$ | $\frac{(b-a)^2}{12}$ | $\frac{e^{tb} - e^{ta}}{t(b-a)}$ |
| **Exponential** | $f(x) = \lambda e^{-\lambda x}$ | $x \geq 0$ | $\frac{1}{\lambda}$ | $\frac{1}{\lambda^2}$ | $\frac{\lambda}{\lambda - t}$ |
| **Normal** | $f(x) = \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{(x-\mu)^2}{2\sigma^2}}$ | $x \in \mathbb{R}$ | $\mu$ | $\sigma^2$ | $e^{t\mu + \frac{1}{2}t^2\sigma^2}$ |
| **Cauchy** | $f(x) = \frac{1}{\pi} \frac{1}{1+x^2}$ | $x \in \mathbb{R}$ | Undefined | Undefined | Undefined |
```

### Exponential Distribution

**Memoryless Property**: For $X \sim \text{Exp}(\lambda)$:
```{math}
P(X > s + t | X > t) = P(X > s) = e^{-\lambda s}
```

**Interpretation**: The probability of surviving an additional $s$ units of time is independent of how long the component has already survived.

### Normal Distribution

**Standard Normal**: $Z \sim N(0,1)$ with CDF $\Phi(z) = P(Z \leq z)$.

**Standardization**: If $X \sim N(\mu, \sigma^2)$, then:
```{math}
Z = \frac{X - \mu}{\sigma} \sim N(0,1)
```

**Probability Calculation**:
```{math}
P(X \leq t) = \Phi\left(\frac{t - \mu}{\sigma}\right)
```

**Symmetric Properties**:
```{math}
\Phi(-z) = 1 - \Phi(z) \quad \text{and} \quad \Phi(0) = 0.5
```

### Cauchy Distribution

Used to model spikes or peaks in large datasets (rare events).

**Note**: Mean and variance are undefined due to heavy tails.

---

## Joint Distributions & Independence

### Joint Distribution Function

For two RVs $X, Y$:
```{math}
F_{X,Y}(a,b) = P(X \leq a, Y \leq b)
```

**Marginal Distributions**:
```{math}
F_X(a) = \lim_{b\to\infty} F_{X,Y}(a,b)
```

### Joint PMF/PDF

**Discrete**:
```{math}
p_{X,Y}(x,y) = P(X = x, Y = y)
```

**Continuous**:
```{math}
f_{X,Y}(x,y) \quad \text{such that } \int\int_{A} f_{X,Y}(x,y) \, dx \, dy = P((X,Y) \in A)
```

**Marginal PDF**:
```{math}
f_X(x) = \int_{-\infty}^{\infty} f_{X,Y}(x,y) \, dy
```

### Independence of Random Variables

$X$ and $Y$ are independent if:
```{math}
F_{X,Y}(a,b) = F_X(a) F_Y(b) \quad \forall a,b
```

**Equivalent Conditions**:
- For discrete: $P(X=x, Y=y) = P(X=x)P(Y=y)$
- For continuous: $f_{X,Y}(x,y) = f_X(x)f_Y(y)$

**Consequences of Independence**:
```{math}
\begin{align*}
\mathbb{E}[XY] &= \mathbb{E}[X]\mathbb{E}[Y] \\
\operatorname{Cov}(X,Y) &= 0 \\
\operatorname{Var}(X+Y) &= \operatorname{Var}(X) + \operatorname{Var}(Y) \\
\phi_{X+Y}(t) &= \phi_X(t) \phi_Y(t)
\end{align*}
```

```{warning}
Uncorrelated ($\operatorname{Cov}(X,Y) = 0$) does **NOT** imply independence (except for jointly normal RVs).
```

### Covariance & Correlation

**Covariance**:
```{math}
\operatorname{Cov}(X,Y) = \mathbb{E}[(X - \mathbb{E}[X])(Y - \mathbb{E}[Y])] = \mathbb{E}[XY] - \mathbb{E}[X]\mathbb{E}[Y]
```

**Correlation Coefficient**:
```{math}
\rho_{X,Y} = \frac{\operatorname{Cov}(X,Y)}{\sqrt{\operatorname{Var}(X)\operatorname{Var}(Y)}} \quad \in [-1, 1]
```

**Properties**:
```{math}
\begin{align*}
\operatorname{Cov}(X,X) &= \operatorname{Var}(X) \\
\operatorname{Cov}(X,Y) &= \operatorname{Cov}(Y,X) \\
\operatorname{Cov}(aX + b, cY + d) &= ac \operatorname{Cov}(X,Y) \\
\operatorname{Var}(X + Y) &= \operatorname{Var}(X) + \operatorname{Var}(Y) + 2\operatorname{Cov}(X,Y)
\end{align*}
```

---

## Conditional Distributions & Expectation

### Conditional PMF/PDF

**Discrete**:
```{math}
P_{X|Y}(x|y) = P(X = x | Y = y) = \frac{P(X = x, Y = y)}{P(Y = y)}
```

**Continuous**:
```{math}
f_{X|Y}(x|y) = \frac{f_{X,Y}(x,y)}{f_Y(y)}
```

### Conditional Expectation

**Discrete**:
```{math}
\mathbb{E}[X|Y = y] = \sum_x x P_{X|Y}(x|y)
```

**Continuous**:
```{math}
\mathbb{E}[X|Y = y] = \int_{-\infty}^{\infty} x f_{X|Y}(x|y) \, dx
```

**Important**: $\mathbb{E}[X|Y]$ is itself a random variable (function of $Y$).

### Law of Total Expectation

```{math}
\mathbb{E}[X] = \mathbb{E}[\mathbb{E}[X|Y]]
```

For discrete $Y$:
```{math}
\mathbb{E}[X] = \sum_y \mathbb{E}[X|Y = y] P(Y = y)
```

For continuous $Y$:
```{math}
\mathbb{E}[X] = \int_{-\infty}^{\infty} \mathbb{E}[X|Y = y] f_Y(y) \, dy
```

### Conditional Variance

```{math}
\operatorname{Var}(X|Y = y) = \mathbb{E}[X^2|Y = y] - (\mathbb{E}[X|Y = y])^2
```

**Law of Total Variance**:
```{math}
\operatorname{Var}(X) = \mathbb{E}[\operatorname{Var}(X|Y)] + \operatorname{Var}(\mathbb{E}[X|Y])
```

### Mean Squared Error (MSE) Minimization

```{theorem} Optimal Estimator
The function $g(Y)$ that minimizes $\mathbb{E}[(X - g(Y))^2]$ is:
\begin{equation*}
g(Y) = \mathbb{E}[X|Y = Y]
\end{equation*}
```

**Proof**: Follows from the orthogonality principle in Hilbert spaces.

---

## Transformation of Random Variables

### General Transformation Formula

For a continuous RV $X$ with density $f_X(x)$ and a **differentiable, strictly monotone** function $g$:

```{math}
Y = g(X) \implies f_Y(y) = f_X(g^{-1}(y)) \cdot \left| \frac{d}{dy} g^{-1}(y) \right| = \frac{f_X(g^{-1}(y))}{|g'(g^{-1}(y))|}
```

**Validity**: Only for $y$ in the range of $g$; $f_Y(y) = 0$ outside this range.

### Example: Exponential Transformation

If $X \sim \text{Unif}([0,1])$ and $Y = e^X$:

```{math}
Y \sim \text{Exp}(1) \text{ on } [1, e] \quad \text{with } f_Y(y) = \frac{1}{y} \text{ for } y \in [1, e]
```

**Verification**: $\int_1^e \frac{1}{y} \, dy = \ln(e) - \ln(1) = 1$.

### Multiple Variables

For $Y_1 = g_1(X_1, X_2)$ and $Y_2 = g_2(X_1, X_2)$ with invertible transformation:

```{math}
f_{Y_1,Y_2}(y_1,y_2) = f_{X_1,X_2}(g_1^{-1}(y_1,y_2), g_2^{-1}(y_1,y_2)) \cdot |J|
```

where $|J|$ is the absolute value of the Jacobian determinant.

---

## Limit Theorems

### Law of Large Numbers (LLN)

**Weak LLN**: For i.i.d. RVs $X_1, X_2, \ldots$ with $\mathbb{E}[X_i] = \mu$ and $\operatorname{Var}(X_i) = \sigma^2 < \infty$:

```{math}
\frac{S_n}{n} = \frac{X_1 + X_2 + \ldots + X_n}{n} \xrightarrow{P} \mu \quad \text{as } n \to \infty
```

**Strong LLN**: Under the same conditions (with finite mean):

```{math}
P\left(\lim_{n\to\infty} \frac{S_n}{n} = \mu\right) = 1 \quad \text{(almost sure convergence)}
```

**Interpretation**: The sample mean converges to the true mean as $n \to \infty$.

### Central Limit Theorem (CLT)

For i.i.d. RVs $X_1, X_2, \ldots$ with $\mathbb{E}[X_i] = \mu$ and $\operatorname{Var}(X_i) = \sigma^2 < \infty$:

```{math}
\frac{S_n - n\mu}{\sigma\sqrt{n}} \xrightarrow{d} N(0,1) \quad \text{as } n \to \infty
```

**Approximation**: For large $n$:

```{math}
S_n \approx N(n\mu, n\sigma^2)
```

**Special Case - Binomial**: If $S_n \sim \text{Bin}(n,p)$:

```{math}
\frac{S_n - np}{\sqrt{np(1-p)}} \xrightarrow{d} N(0,1)
```

### Chebyshev's Inequality

For any RV $X$ with $\mathbb{E}[X] = \mu$ and $\operatorname{Var}(X) = \sigma^2$:

```{math}
P(|X - \mu| \geq \varepsilon) \leq \frac{\sigma^2}{\varepsilon^2} \quad \forall \varepsilon > 0
```

**Application**: Provides a bound on the probability of deviation from the mean.

**Example**: For $S_n \sim \text{Bin}(n,p)$:

```{math}
P(|S_n - np| \geq \varepsilon) \leq \frac{np(1-p)}{\varepsilon^2} \leq \frac{n}{4\varepsilon^2}
```

### Markov's Inequality

For any **non-negative** RV $X$:

```{math}
P(X \geq a) \leq \frac{\mathbb{E}[X]}{a} \quad \forall a > 0
```

---

## Stochastic Processes

### Definition

A **stochastic process** is a collection of RVs $X = \{X_t: t \in T\}$ where $T$ is an index set (usually time).

**Representation**:
```{math}
X: T \times \Omega \to \mathbb{R} \quad \text{via } (t, \omega) \mapsto X_t(\omega)
```

### Characterization

A stochastic process is characterized by its **finite-dimensional distributions**:

```{math}
F_{X_{t_1}, \ldots, X_{t_k}}(x_1, \ldots, x_k) = P(X_{t_1} \leq x_1, \ldots, X_{t_k} \leq x_k)
```

for all $k \geq 1$ and $t_1 < t_2 < \ldots < t_k$.

### Mean & Correlation Functions

**Mean Function**:
```{math}
m_X(t) = \mathbb{E}[X_t]
```

**Correlation Function**:
```{math}
R_X(t_1, t_2) = \mathbb{E}[X_{t_1} X_{t_2}]
```

**Covariance Function**:
```{math}
C_X(t_1, t_2) = R_X(t_1, t_2) - m_X(t_1) m_X(t_2)
```

### Stationary Processes

**Definition**: A process is **stationary** if its finite-dimensional distributions are invariant under time shifts:

```{math}
(X_{t_1}, \ldots, X_{t_k}) \stackrel{d}{=} (X_{t_1+s}, \ldots, X_{t_k+s}) \quad \forall s
```

**Wide-Sense Stationary (WSS)**:
- Constant mean: $m_X(t) = m$ for all $t$
- Correlation depends only on time difference: $R_X(t_1, t_2) = R_X(|t_2 - t_1|)$

### Examples of Stochastic Processes

| Process | Description | Mean | Variance | Correlation |
|---------|-------------|------|----------|-------------|
| **Bernoulli** | $X_n$ i.i.d. $\pm 1$ valued | $2p-1$ | $4p(1-p)$ | $(2p-1)^2$ for $t_1\neq t_2$ |
| **Random Walk** | $X_n = \sum_{i=1}^n B_i$ | $0$ (if $p=1/2$) | $n$ | $\min(t_1, t_2)$ |
| **Brownian Motion** | Continuous limit of RW | $0$ | $t$ | $\min(t_1, t_2)$ |
| **Poisson** | Counts events in time | $\lambda t$ | $\lambda t$ | $\lambda \min(t_1, t_2)$ |

#### Bernoulli Process

$X_n$ i.i.d. with $P(X_n = 1) = p$ and $P(X_n = -1) = 1-p$.

#### Random Walk (RW)

$X_0 = 0$, $X_n = X_{n-1} + B_n$ where $B_n$ i.i.d. $\pm 1$ valued.

- **Symmetric RW**: $p = 1/2$
- **Recurrence**: In $d=1,2$, RW is recurrent (returns to origin infinitely often) with probability 1
- **Transience**: In $d \geq 3$, RW is transient (never returns to origin) with probability 1

**CLT for RW**:
```{math}
\frac{X_n}{\sqrt{n}} \xrightarrow{d} N(0,1) \quad \text{for symmetric RW}
```

#### Brownian Motion (BM)

- Models particle movement in a liquid (Einstein, 1905)
- Models stock market fluctuations (Bachelier, 1900)
- Continuous paths, nowhere differentiable
- $B_t \sim N(0,t)$ for each $t$
- Independent increments

**Connection to RW**: Scaled limit of symmetric RW as step size $\to 0$ and time $\to \infty$.

#### Poisson Process

$N_t$ counts the number of events in $[0,t]$ for a process with:

1. $N_0 = 0$
2. Independent increments
3. $N_{s+t} - N_s \sim \text{Pois}(\lambda t)$

**Properties**:
- $\mathbb{E}[N_t] = \lambda t$
- $\operatorname{Var}(N_t) = \lambda t$
- $C_N(t_1, t_2) = \lambda \min(t_1, t_2)$
- Inter-arrival times $T_i \sim \text{Exp}(\lambda)$ and independent

**Thinning Property**: If each event is kept with probability $p$, the thinned process is $\text{PP}(p\lambda)$.

**Merging Property**: Sum of independent $\text{PP}(\lambda_1)$ and $\text{PP}(\lambda_2)$ is $\text{PP}(\lambda_1 + \lambda_2)$.

#### Random Telegraph Process

$X_t = (-1)^{N_t}$ where $N_t$ is a Poisson process.

**Mean**: $\mathbb{E}[X_t] = e^{-2\lambda t}$

**Correlation**: $R_X(t_1, t_2) = e^{-2\lambda |t_2 - t_1|}$

---

## Markov Chains

### Definition

A **Markov Chain (MC)** is a discrete-time stochastic process with the **Markov Property**:

```{math}
P(X_{n+1} = x_{n+1} | X_n = x_n, X_{n-1} = x_{n-1}, \ldots, X_0 = x_0) = P(X_{n+1} = x_{n+1} | X_n = x_n)
```

**Interpretation**: Given the present, the future is independent of the past.

### Transition Probabilities

**One-step**:
```{math}
p_{ij} = P(X_{n+1} = j | X_n = i)
```

**Transition Matrix**:
```{math}
P = \begin{pmatrix} p_{11} & p_{12} & \cdots & p_{1k} \\ p_{21} & p_{22} & \cdots & p_{2k} \\ \vdots & \vdots & \ddots & \vdots \\ p_{k1} & p_{k2} & \cdots & p_{kk} \end{pmatrix}
```

**Properties**: $p_{ij} \geq 0$ and $\sum_j p_{ij} = 1$ for all $i$ (stochastic matrix).

**m-step**:
```{math}
p_{ij}^{(m)} = P(X_{n+m} = j | X_n = i)
```

**Chapman-Kolmogorov Equations**:
```{math}
p_{ij}^{(m+n)} = \sum_{k \in S} p_{ik}^{(m)} p_{kj}^{(n)}
```

**Matrix Form**: $P^{(m+n)} = P^m P^n$ and $P^{(m)} = P^m$.

### Classification of States

- **Accessible**: $i \to j$ if $p_{ij}^{(n)} > 0$ for some $n \geq 0$
- **Communicating**: $i \leftrightarrow j$ if $i \to j$ and $j \to i$
- **Communication Classes**: Equivalence classes under $\leftrightarrow$
- **Irreducible**: All states communicate (single communication class)
- **Period**: $d_i = \gcd\{n \geq 1: p_{ii}^{(n)} > 0\}$
- **Aperiodic**: $d_i = 1$ for all $i$

### Stationary Distributions

A probability vector $\vec{\pi} = (\pi_1, \pi_2, \ldots)$ is a **stationary distribution** if:

```{math}
\vec{\pi} = \vec{\pi} P \quad \text{and} \quad \sum_i \pi_i = 1, \pi_i \geq 0
```

**Interpretation**: If $X_0 \sim \vec{\pi}$, then $X_n \sim \vec{\pi}$ for all $n$.

**Existence**:
- Finite state space + irreducible $\Rightarrow$ unique stationary distribution
- Finite state space + irreducible + aperiodic $\Rightarrow$ unique stationary distribution and convergence

### Convergence

```{theorem} Fundamental Theorem of Markov Chains
If a Markov Chain is **irreducible** and **aperiodic** with a **finite** state space, then:
\begin{itemize}
\item There exists a **unique** stationary distribution $\vec{\pi}$
\item For **any** initial distribution $\vec{\nu}$:
\begin{equation*}
\vec{\nu} P^n \xrightarrow{n\to\infty} \vec{\pi}
\end{equation*}
\end{itemize}
```

**Corollary**: Every row of $P^n$ converges to $\vec{\pi}$ as $n \to \infty$.

### PageRank Algorithm

**Problem**: Rank web pages based on link structure.

**Model**: Random surfer model with:
- Follows links with probability $\alpha \approx 0.85$
- Teleports to random page with probability $1-\alpha$

**Google Matrix**:
```{math}
G = \alpha S + (1-\alpha) \frac{1}{n} \vec{e} \vec{e}^T
```

where $S$ is the stochastic matrix from the web graph (with fixes for dangling nodes).

**Properties**:
- $G$ is irreducible and aperiodic (since $G > 0$)
- Converges to unique stationary distribution (PageRank vector)

**Dangling Nodes**: Pages without outlinks. Solution: Add uniform row.

**Rank Sinks**: Groups of pages that trap the random surfer. Solution: Use teleportation.

---

## Continuous-Time Markov Chains

### Holding Times

For a continuous-time MC, the time spent in state $i$ before jumping:

- **Memoryless**: $P(T_i > s + t | T_i > t) = P(T_i > s)$
- **Distribution**: $T_i \sim \text{Exp}(\nu_i)$ for some $\nu_i > 0$

### Poisson Process (Special Case)

A counting process $N_t$ is a **Poisson Process** with rate $\lambda > 0$ if:

1. $N_0 = 0$
2. Independent increments
3. $N_{s+t} - N_s \sim \text{Pois}(\lambda t)$

**Key Properties**:
- $N_t \sim \text{Pois}(\lambda t)$
- $\mathbb{E}[N_t] = \lambda t$
- $\operatorname{Var}(N_t) = \lambda t$
- Inter-arrival times $T_i \sim \text{Exp}(\lambda)$ and independent

**Construction**: If $T_i \sim \text{Exp}(\lambda)$ i.i.d., then $N_t = \max\{n: \sum_{i=1}^n T_i \leq t\}$ is a Poisson process.

---

## Prerequisite Mathematical Tools

### Calculus Rules

#### Differentiation Rules

| Rule | Formula |
|------|---------|
| **Power Rule** | $\frac{d}{dx} x^n = n x^{n-1}$ |
| **Exponential** | $\frac{d}{dx} e^{ax} = a e^{ax}$ |
| **Natural Log** | $\frac{d}{dx} \ln(x) = \frac{1}{x}$ |
| **Product Rule** | $\frac{d}{dx} [f(x)g(x)] = f'(x)g(x) + f(x)g'(x)$ |
| **Quotient Rule** | $\frac{d}{dx} \left[\frac{f(x)}{g(x)}\right] = \frac{f'(x)g(x) - f(x)g'(x)}{[g(x)]^2}$ |
| **Chain Rule** | $\frac{d}{dx} f(g(x)) = f'(g(x)) \cdot g'(x)$ |

#### Integration Rules

| Rule | Formula |
|------|---------|
| **Power Rule** | $\int x^n dx = \frac{x^{n+1}}{n+1} + C$ (for $n \neq -1$) |
| **Exponential** | $\int e^{ax} dx = \frac{1}{a} e^{ax} + C$ |
| **Natural Log** | $\int \frac{1}{x} dx = \ln|x| + C$ |
| **Integration by Parts** | $\int u dv = uv - \int v du$ |

**Integration by Parts Example**:
```{math}
\int x e^{ax} dx = \frac{x e^{ax}}{a} - \frac{1}{a} \int e^{ax} dx = \frac{e^{ax}}{a^2} (a x - 1) + C
```

### Special Integrals

```{math}
\begin{align*}
\int_{-\infty}^{\infty} e^{-x^2} dx &= \sqrt{\pi} \\
\int_0^{\infty} x^n e^{-ax} dx &= \frac{n!}{a^{n+1}} \quad \text{(Gamma function: } \Gamma(n+1) = n!) \\
\int_0^{\infty} e^{-ax} dx &= \frac{1}{a} \quad \text{for } a > 0 \\
\int_0^{\infty} x e^{-ax} dx &= \frac{1}{a^2} \\
\int_0^{\infty} x^2 e^{-ax} dx &= \frac{2}{a^3}
\end{align*}
```

### Taylor Series

```{math}
\begin{align*}
e^x &= \sum_{n=0}^{\infty} \frac{x^n}{n!} = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \ldots \\
\ln(1+x) &= \sum_{n=1}^{\infty} (-1)^{n+1} \frac{x^n}{n} = x - \frac{x^2}{2} + \frac{x^3}{3} - \ldots \quad \text{for } |x| < 1 \\
\sin(x) &= \sum_{n=0}^{\infty} (-1)^n \frac{x^{2n+1}}{(2n+1)!} = x - \frac{x^3}{3!} + \frac{x^5}{5!} - \ldots \\
\cos(x) &= \sum_{n=0}^{\infty} (-1)^n \frac{x^{2n}}{(2n)!} = 1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \ldots \\
e^{x} &\approx 1 + x + \frac{x^2}{2} \quad \text{(2nd order Taylor)}
\end{align*}
```

### Common Series

```{math}
\begin{align*}
\sum_{k=0}^{\infty} r^k &= \frac{1}{1-r} \quad \text{for } |r| < 1 \\
\sum_{k=1}^{\infty} k r^{k-1} &= \frac{1}{(1-r)^2} \quad \text{for } |r| < 1 \\
\sum_{k=1}^{\infty} k^2 r^{k-1} &= \frac{1+r}{(1-r)^3} \quad \text{for } |r| < 1 \\
\sum_{k=1}^{n} k &= \frac{n(n+1)}{2} \\
\sum_{k=1}^{n} k^2 &= \frac{n(n+1)(2n+1)}{6} \\
\sum_{k=1}^{\infty} \frac{1}{k^2} &= \frac{\pi^2}{6} \quad \text{(Basel problem)} \\
H_n &= \sum_{k=1}^n \frac{1}{k} \approx \ln(n) + \gamma \quad \text{where } \gamma \approx 0.5772
\end{align*}
```

---

## Important Examples from Exercises

### Conditional Probability Examples

**Example 1**: Two dice, sum equals 6 vs. first die equals 4
- $E_1$: sum equals 6, $P(E_1) = \frac{5}{36}$
- $E_3$: first die equals 4, $P(E_3) = \frac{1}{6}$
- $P(E_1 | E_3) = \frac{1}{6} > P(E_1)$ (dependent!)
- $P(E_2 | E_3) = \frac{1}{6} = P(E_2)$ (independent!)

**Example 2**: Lottery probabilities
- Probability of winning with 6 out of 48: $P = \frac{1}{\binom{48}{6}} \approx 1.2 \times 10^{-7}$
- Probability that at least one of $H$ participants wins: $1 - \left(1 - \frac{1}{\binom{48}{6}}\right)^H$

### Conditional Expectation Examples

**Exercise from Week 8**: Given joint density $f_{X,Y}(x,y) = 6xy(2-x-y)$ for $0 < x,y < 1$:

```{math}
\mathbb{E}[X|Y=y] = \frac{5 - 4y}{2(4 - 3y)} \quad \text{for } 0 < y < 1
```

### Variance Calculation

**Exercise from Week 8**: For $f_{X,Y}(x,y) = \frac{1}{18} e^{-(x+y)}$ for $0 < y < x$:

```{math}
\operatorname{Var}(X|Y=2) = 36
```

### Geometric Distribution Proof

**Exercise from Week 8**: If $X \sim \text{Pois}(Y)$ and $Y \sim \text{Exp}(\lambda)$, then $W = X + 1 \sim \text{Geom}\left(\frac{\lambda}{\lambda+1}\right)$.

### Markov Chain Examples

**Example**: Gambler's Ruin
- States: $\{0, 1, 2, 3\}$ (0 and 3 are absorbing)
- Communication classes: $\{0\}, \{1,2\}, \{3\}$
- Not irreducible (multiple classes)

**Example**: Simple Two-State Chain
- States: $\{1, 2\}$
- Transition matrix: $P = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}$
- Stationary distribution: $\vec{\pi} = (1/2, 1/2)$
- Periodic with period 2

### Poisson Process Examples

**Example**: Machine failures with rate $\lambda = 2$ per week.

- $P(\text{no failure in 2 weeks}) = e^{-4}$
- $P(\text{at most 1 failure in 2 weeks}) = e^{-4} + 4e^{-4} = 5e^{-4}$
- $P(\text{inter-arrival > 5 weeks}) = e^{-10}$

---

## Exam-Ready Formula Sheet

### Probability

```{math}
\begin{align*}
P(E|F) &= \frac{P(E \cap F)}{P(F)} & P(E) &= P(E|A)P(A) + P(E|A^c)P(A^c) \\
P(A|E) &= \frac{P(E|A)P(A)}{P(E)} & P(A \cap B) &= P(A)P(B|A) = P(B)P(A|B)
\end{align*}
```

### Expectation & Variance

```{math}
\begin{align*}
\mathbb{E}[X] &= \sum x P(X=x) & \mathbb{E}[X] &= \int x f_X(x) dx \\
\operatorname{Var}(X) &= \mathbb{E}[X^2] - (\mathbb{E}[X])^2 & \operatorname{Var}(aX+b) &= a^2 \operatorname{Var}(X) \\
\operatorname{Cov}(X,Y) &= \mathbb{E}[XY] - \mathbb{E}[X]\mathbb{E}[Y] & \rho_{X,Y} &= \frac{\operatorname{Cov}(X,Y)}{\sqrt{\operatorname{Var}(X)\operatorname{Var}(Y)}}
\end{align*}
```

### Distributions

```{math}
\begin{align*}
\text{Binomial: } P(X=k) &= \binom{n}{k} p^k (1-p)^{n-k} & \mathbb{E}[X] &= np, \operatorname{Var}(X) = np(1-p) \\
\text{Poisson: } P(X=k) &= \frac{\lambda^k e^{-\lambda}}{k!} & \mathbb{E}[X] = \lambda, \operatorname{Var}(X) = \lambda \\
\text{Geometric: } P(X=k) &= (1-p)^{k-1} p & \mathbb{E}[X] = 1/p, \operatorname{Var}(X) = (1-p)/p^2 \\
\text{Normal: } f(x) &= \frac{1}{\sqrt{2\pi\sigma^2}} e^{-(x-\mu)^2/(2\sigma^2)} & \mathbb{E}[X] = \mu, \operatorname{Var}(X) = \sigma^2 \\
\text{Exp: } f(x) &= \lambda e^{-\lambda x} & \mathbb{E}[X] = 1/\lambda, \operatorname{Var}(X) = 1/\lambda^2
\end{align*}
```

### Limit Theorems

```{math}
\begin{align*}
\text{LLN: } \frac{S_n}{n} &\xrightarrow{P} \mu & \text{CLT: } \frac{S_n - n\mu}{\sigma\sqrt{n}} &\xrightarrow{d} N(0,1) \\
\text{Chebyshev: } P(|X-\mu| \geq \varepsilon) &\leq \frac{\sigma^2}{\varepsilon^2} & \text{Markov: } P(X \geq a) &\leq \frac{\mathbb{E}[X]}{a}
\end{align*}
```

### Markov Chains

```{math}
\begin{align*}
\text{Markov: } P(X_{n+1}|X_n, \ldots, X_0) &= P(X_{n+1}|X_n) & \text{Chapman-Kolmogorov: } p_{ij}^{(m+n)} &= \sum_k p_{ik}^{(m)} p_{kj}^{(n)} \\
\text{Stationary: } \vec{\pi} &= \vec{\pi} P & \text{Convergence: } \vec{\nu} P^n &\to \vec{\pi}
\end{align*}
```

### Stochastic Processes

```{math}
\begin{align*}
\text{Mean: } m_X(t) &= \mathbb{E}[X_t] & \text{Correlation: } R_X(t_1,t_2) &= \mathbb{E}[X_{t_1}X_{t_2}] \\
\text{Covariance: } C_X(t_1,t_2) &= R_X(t_1,t_2) - m_X(t_1)m_X(t_2) & \text{Stationary: } R_X(t_1,t_2) &= R_X(|t_2-t_1|)
\end{align*}
```

---

## Key Takeaways

### Most Important Concepts

1. **Probability Space & Axioms**: Foundation of all probability theory
2. **Conditional Probability**: Essential for Bayesian reasoning
3. **Expectation & Variance**: Fundamental measures of central tendency and spread
4. **Limit Theorems**: LLN and CLT are the most important results in probability
5. **Markov Property**: Foundation for Markov Chains and many stochastic processes
6. **Stationary Distributions**: Long-term behavior of Markov Chains
7. **Poisson Process**: Fundamental continuous-time stochastic process

### Common Pitfalls

```{warning} Common Mistakes
- **Independence vs. Uncorrelated**: Independent implies uncorrelated, but not vice versa (except for jointly normal RVs)
- **Continuous vs. Discrete**: Remember to use PMF for discrete and PDF for continuous RVs
- **Conditional Probability**: Always check that $P(F) > 0$ before using $P(E|F)$
- **Expectation of Functions**: $\mathbb{E}[g(X)] \neq g(\mathbb{E}[X])$ in general (Jensen's inequality)
- **Variance of Sums**: $\operatorname{Var}(X+Y) = \operatorname{Var}(X) + \operatorname{Var}(Y) + 2\operatorname{Cov}(X,Y)$
- **Markov Chain Convergence**: Requires **both** irreducibility **and** aperiodicity
```

### Problem-Solving Strategies

1. **Identify the Distribution**: Recognize which distribution the problem involves
2. **Use Definitions**: Start with the definition (PMF, PDF, or property)
3. **Check Conditions**: Verify all conditions are met before applying theorems
4. **Use Linearity**: Expectation is linear - use this whenever possible
5. **Conditioning**: Break complex problems into simpler conditional problems
6. **Symmetry**: Look for symmetry to simplify calculations
7. **Approximations**: Use CLT for large $n$ approximations
