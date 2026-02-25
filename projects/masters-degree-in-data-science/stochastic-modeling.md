---
title: Stochastic Modeling
subtitle: Lecture Notes
subject: Probability Theory and Stochastic Processes
authors:
  - name: Erich Baur
    affiliation: ZHAW School of Engineering
---

## Basic Definitions

### Random Events

:::{prf:definition} Random Experiment & Sample Space
:label: def-experiment

A **random experiment** is an experiment whose outcome is not exactly known in advance. The set $\Omega$ of all possible outcomes is called the **sample space**.

A **(random) event** is a collection of outcomes—in other words, a subset $A \subseteq \Omega$. We usually write $\mathcal{A}$ for the set of all events on $\Omega$.
:::

**Occurrence:** The event $A$ occurs if the outcome of the experiment belongs to $A$.

:::{list-table} Examples of Sample Spaces
:header-rows: 1
:widths: 30 70

* - Experiment
  - Sample Space $\Omega$
* - Tossing a die
  - $\{1, 2, 3, 4, 5, 6\}$
* - Arrival time of a train
  - $[0\text{h}00; 24\text{h}00[$
:::

#### Special Events
- $A \cap B$: $A$ and $B$ (intersection)
- $A \cup B$: $A$ or $B$ (non-exclusive "or")
- $B \setminus A$: $B$ without $A$ (set difference)
- $A^c = \Omega \setminus A$: the complementary event "not $A$"
- $\bigcap_{i=1}^\infty A_i$: all $A_i$ occur
- $\bigcup_{i=1}^\infty A_i$: at least one $A_i$ occurs

:::{prf:remark}
:label: rem-disjoint
1. If $A \cap B = \emptyset$, we say $A$ and $B$ are **disjoint**, written $A \mathbin{\dot{\cup}} B$.
2. If $A \subseteq B$, event $A$ is said to **imply** event $B$.
3. Note that $A \cup A^c = \Omega$ and $A \cap A^c = \emptyset$.
:::

:::{exercise}
:label: ex-die-events
A die is tossed. Consider the events $A = \{2\}$, $B = \{2, 4, 6\}$, and $C = \{1, 2\}$. Determine the events $B \cap C$, $A \cup B$, and $B \setminus C$.
:::

### Probability Measure

:::{prf:definition} Probability Measure (Kolmogorov Axioms)
:label: def-probability-measure

A probability measure on $\Omega$ is a function $P: \mathcal{A} \to \mathbb{R}$ satisfying:

1. **A1:** $0 \leq P(E) \leq 1$ for all events $E \in \mathcal{A}$.
2. **A2:** $P(\Omega) = 1$.
3. **A3:** For every sequence of mutually disjoint events $E_1, E_2, \ldots$:
   $$P\left(\bigcup_{i=1}^{\infty} E_i\right) = \sum_{i=1}^{\infty} P(E_i)$$
:::

:::{prf:proposition}
:label: prop-prob-cons

Let $A, B \subseteq \Omega$ be events and $P$ a probability measure. Then:
- $P(\emptyset) = 0$
- $P(A^c) = 1 - P(A)$
- $P(A \setminus B) = P(A) - P(A \cap B)$
- $P(A \cup B) = P(A) + P(B) - P(A \cap B)$
- If $A \subseteq B$, then $P(A) \leq P(B)$
:::

### Conditional Probabilities

:::{prf:definition} Conditional Probability
:label: def-conditional

Let $P$ be a probability measure on $\Omega$, and let $E$ and $F$ be two events with $P(F) > 0$. The **conditional probability** of $E$ given $F$ is defined as:
$$P(E \mid F) := \frac{P(E \cap F)}{P(F)}$$
:::

:::{prf:theorem} Law of Total Probability
:label: thm-total-prob

Let $\{A_k\}_{k=1}^n$ be a finite partition of the sample space $\Omega$. For any arbitrary event $E$:
$$P(E) = \sum_{k=1}^n P(E \mid A_k)P(A_k)$$
:::

:::{prf:theorem} Bayes' Rule
:label: bayes-rule

If we partition $\Omega$ into events $A$ and $A^c$, the likelihood of $A$ given event $E$ is:
$$P(A \mid E) = \frac{P(E \mid A)P(A)}{P(E \mid A)P(A) + P(E \mid A^c)P(A^c)}$$ (bayes-rule)
:::

:::{prf:example} Monty Hall Problem
:label: ex-monty-hall

Imagine you pick door 1; the host opens door 3, revealing no prize. Should you switch to door 2?
- $H_i$: Prize is behind door $i$. $P(H_i) = 1/3$.
- $D=3$: host opens door 3.
- Probabilities: $P(D=3 \mid H_1) = 1/2$, $P(D=3 \mid H_2) = 1$, $P(D=3 \mid H_3) = 0$.

Using {eq}`bayes-rule`:
$$P(H_1 \mid D=3) = \frac{(1/2)(1/3)}{1/2} = 1/3, \quad P(H_2 \mid D=3) = \frac{1(1/3)}{1/2} = 2/3$$
**Conclusion:** You should switch to door 2 to double your chances of winning.
:::

## Independence

Informally, two events are independent if the occurrence of one does not influence the other.

```{admonition} Definition: Independent Events
:class: tip
Two events $E$ and $F$ are independent if and only if:
$$P(E \cap F) = P(E)P(F)$$
```

### Properties of Independence
1. $E$ and $F$ are independent if $P(E|F) = P(E)$ or $P(F|E) = P(F)$.
2. If $E$ and $F$ are independent, then their complements ($E^c, F^c$) are also independent.

## Random Variables

A random variable (RV) $X$ is a function that maps the sample space of a random experiment to the real numbers: $X: \Omega \to \mathbb{R}$.

### Classification of RVs

| Type | Definition | Key Characteristic |
| :--- | :--- | :--- |
| **Discrete** | Takes finite or countable values | Defined by Probability Mass Function (PMF) $P(X = x_i)$ |
| **Continuous** | Takes values in an uncountable set | Defined by Probability Density Function (PDF) $f_X(x)$ |

### Moments and Functions

The following quantities describe the behavior of a random variable $X$:

- **Distribution Function (CDF):** $F_X(t) = P(X \le t)$
- **Expectation (Mean):** $E[X] = \int x f_X(x) dx$ (or sum for discrete)
- **Variance:** $Var(X) = E[X^2] - (E[X])^2$
- **Moment Generating Function (MGF):** $\phi_X(t) = E[e^{tX}]$

## Discrete Probability Distributions

### Bernoulli Distribution
Models a single trial with success probability $p$.
- **Notation:** $X \sim \text{Ber}(p)$
- $E[X] = p$
- $Var(X) = p(1-p)$

### Binomial Distribution
Models the number of successes in $n$ independent Bernoulli trials.
- **Notation:** $X \sim \text{Bin}(n, p)$
- **PMF:** $P(X=k) = \binom{n}{k} p^k (1-p)^{n-k}$
- $E[X] = np$
- $Var(X) = np(1-p)$
