# Stochastic Modeling

:::{note} Historical Context
**1654**: Blaise Pascal and Pierre de Fermat  
Chevalier de Méré wrote a letter to Pascal, which became the origin of probability theory stemming from gambling problems.

**1932**: Kolmogorov strictly defined probability theory.
:::

## Review of Probability Theory

Modeling of a random experiment involves three key components:

- **Sample space** $\Omega$: the set of possible outcomes
- **Events** $A \subseteq \Omega$: where $\mathcal{A}$ is the set of all measurable events
- **Probability Measure** $\mathbb{P}$: see definition below

### Definition of a Probability Measure

:::{prf:definition} Probability Measure
:label: def-prob-measure

A function $\mathbb{P}: \mathcal{A} \rightarrow \mathbb{R}$ with the following three properties:

**A1)** $0 \le \mathbb{P}(E) \le 1$ for any $E \in \mathcal{A}$

**A2)** $\mathbb{P}(\Omega) = 1$

**A3)** If $E_1, E_2, \dots$ are pairwise disjoint events (i.e., $E_i \cap E_j = \emptyset$ if $i \neq j$), then

$$
\mathbb{P}\left(\bigcup_{i=1}^{\infty} E_i\right) = \sum_{i=1}^{\infty} \mathbb{P}(E_i)
$$ (eq:countable-additivity)

Any function satisfying A1, A2, A3 is called a **Probability Function**. These axioms (A1–A3) are known as the **Kolmogorov Axioms**.
:::

:::{note} Interpretation
- $\mathbb{P}(E) = 0$: almost impossible
- $\mathbb{P}(E) = 1$: almost certain
:::

### Example: Fair Die Tossing

:::{prf:example} Fair Die
:label: ex-fair-die

Consider a fair six-sided die:

- Sample space: $\Omega = \{1, 2, 3, 4, 5, 6\}$
- Event space: $\mathcal{A} = \mathcal{P}(\Omega)$ (power set with $|\mathcal{A}| = |\mathcal{P}(\Omega)| = 2^6$)
- Probability: $\mathbb{P}(\{i\}) = \frac{1}{6}$ for $i=1, \dots, 6$

Let $A = \{2, 4, 6\}$ be the event "roll an even number". Then:

$$
\mathbb{P}(A) \stackrel{\text{A3}}{=} \mathbb{P}(\{2\}) + \mathbb{P}(\{4\}) + \mathbb{P}(\{6\}) = \frac{3}{6} = \frac{1}{2}
$$

This follows the classical probability formula:

$$
\mathbb{P}(A) = \frac{\text{# of favorable outcomes}}{\text{# of all outcomes}}
$$
:::

### Properties of a Probability Measure

:::{prf:proposition} Basic Properties
:label: prop-prob-properties

For any probability measure $\mathbb{P}$ and events $A, B \in \mathcal{A}$:

a) $\mathbb{P}(\emptyset) = 0$

b) $\mathbb{P}(A^c) = 1 - \mathbb{P}(A)$

c) $\mathbb{P}(A \setminus B) = \mathbb{P}(A) - \mathbb{P}(A \cap B)$

d) $\mathbb{P}(A \cup B) = \mathbb{P}(A) + \mathbb{P}(B) - \mathbb{P}(A \cap B)$

e) $\mathbb{P}(A) \le \mathbb{P}(B)$ if $A \subseteq B$
:::

:::{prf:proof}
We prove properties (a) and (b):

**Part (a):** 

$$
1 \stackrel{\text{A2}}{=} \mathbb{P}(\Omega) = \mathbb{P}(\Omega \cup \emptyset) \stackrel{\text{A3}}{=} \mathbb{P}(\Omega) + \mathbb{P}(\emptyset) \stackrel{\text{A2}}{=} 1 + \mathbb{P}(\emptyset)
$$

Therefore, $\mathbb{P}(\emptyset) = 0$.

**Part (b):** Since $\Omega = A \cup A^c$ and the events are disjoint, we have:

$$
1 = \mathbb{P}(\Omega) = \mathbb{P}(A) + \mathbb{P}(A^c)
$$

Therefore, $\mathbb{P}(A^c) = 1 - \mathbb{P}(A)$.

The remaining properties follow similarly.
:::

## Conditional Probabilities

Consider events $E, F \in \mathcal{A}$ with $\mathbb{P}(F) > 0$.

**Question:** What is the probability of $E$ if we know that $F$ occurs?

- Relevant cases: $\omega \in F$
- Favorable cases: $\omega \in E \cap F$

:::{prf:definition} Conditional Probability
:label: def-conditional-prob

The **conditional probability** of $E$ given $F$ is defined as:

$$
\mathbb{P}(E|F) = \frac{\mathbb{P}(E \cap F)}{\mathbb{P}(F)}
$$ (eq:conditional-prob)
:::

### Example: Throwing Two Dice

:::{prf:example} Two Dice
:label: ex-two-dice

Sample space: $\Omega = \{(i, j) : i, j = 1, 2, \dots, 6\}$

Let $E$ be the event "sum equals 6". Then $\mathbb{P}(E) = \frac{5}{36}$.

Now assume we know that $F$ = "first toss equals 2". Then:

- $\mathbb{P}(F) = \frac{1}{6}$
- $\mathbb{P}(E \cap F) = \mathbb{P}(\{(2,4)\}) = \frac{1}{36}$

Therefore:

$$
\mathbb{P}(E|F) = \frac{\mathbb{P}(E \cap F)}{\mathbb{P}(F)} = \frac{1/36}{1/6} = \frac{1}{6} \quad \left[ > \frac{5}{36} \right]
$$

Notice that knowing the first die increases the probability of the sum being 6.
:::

:::{important} Multiplication Rule
From the definition of conditional probability, we obtain:

$$
\mathbb{P}(E \cap F) = \mathbb{P}(F) \cdot \mathbb{P}(E|F)
$$ (eq:multiplication-rule)
:::

## Law of Total Probability

:::{prf:theorem} Law of Total Probability (General Form)
:label: thm-total-prob

Let $\{A_1, A_2, \dots, A_n\}$ be a partition of $\Omega$, i.e., $\Omega = A_1 \cup A_2 \cup \dots \cup A_n$ with pairwise disjoint sets.

For any event $E \in \mathcal{A}$:

$$
E = E \cap \Omega = E \cap (A_1 \cup A_2 \cup \dots \cup A_n)
$$

Therefore:

$$
\mathbb{P}(E) \stackrel{\text{A3}}{=} \sum_{i=1}^{n} \mathbb{P}(E \cap A_i) = \sum_{i=1}^{n} \mathbb{P}(E|A_i) \cdot \mathbb{P}(A_i)
$$ (eq:total-prob)
:::

:::{prf:theorem} Simplified Law of Total Probability
:label: thm-total-prob-simple

For any event $A$ with $\mathbb{P}(A) > 0$, we have the partition $\Omega = A \cup A^c$. Thus:

$$
\mathbb{P}(E) = \mathbb{P}(E|A) \cdot \mathbb{P}(A) + \mathbb{P}(E|A^c) \cdot \mathbb{P}(A^c)
$$ (eq:total-prob-simple)
:::
