---
title: Stochastic Modeling
subtitle: Lecture Notes
subject: Probability Theory and Stochastic Processes
authors:
  - name: Erich Baur
    affiliation: ZHAW School of Engineering
---

## Basic definitions

### Random events

:::{prf:definition} Random Experiment and Sample Space
:label: def-random-experiment

A **random experiment** is an experiment whose outcome is not exactly known in advance.

The set $\Omega$ of all possible outcomes of a given random experiment is called the **sample space**.

A **(random) event** is a collection of outcomes - in other words a subset $A \subseteq \Omega$ of $\Omega$. We usually write $\mathcal{A}$ for the set of all events on $\Omega$.

**Occurrence**: The event $A$ occurs if the outcome of the experiment belongs to $A$.
:::

:::{prf:example} Sample Spaces and Events
:label: ex-sample-spaces
:class: dropdown

1. **Tossing a die**: $\Omega = \{1, 2, 3, 4, 5, 6\}$
   - Event $A = \{2, 4, 6\}$: "toss an even number"
   - If the outcome is 4, then the event $A$ occurred.

2. **Exact arrival time of a train**: $\Omega = [0h00; 24h00[$
   - Event $A = [12h55; 13h05]$: "arrival between 12h55 and 13h05"
   - If the train arrived at 13h00, then the event $A$ occurred.
:::

#### Special events

The following operations on events are fundamental:

- $A \cap B$: $A$ and $B$
- $A \cup B$: $A$ or $B$ (non-exclusive "or")
- $B \setminus A$: $B$ without $A$
- $A^c = \Omega \setminus A$: the complementary event "not $A$"
- $\bigcap_{i=1}^{\infty} A_i$: all $A_i$
- $\bigcup_{i=1}^{\infty} A_i$: at least one $A_i$


#### Remarks

1. If $A \cap B = \emptyset$, we say that $A$ and $B$ are **disjoint**. We often write $A \dot{\cup} B$ to indicate a union of two disjoint events $A, B$.

2. When $A \subseteq B$, event $A$ is said to **imply** event $B$. We then have $A \cap B = A$ and $A \cup B = B$.

3. Note that we have $A \cup A^c = \Omega$ and $A \cap A^c = \emptyset$.

:::{prf:example} Set Operations on Events
:label: ex-set-operations
:class: dropdown

If $A = \{3, 5, 6\}$ and $B = \{1, 3\}$, then:
- $A \cup B = \{1, 3, 5, 6\}$
- $A \cap B = \{3\}$
- $A^c = \{1, 2, 4\}$
:::

:::{exercise} Set Operations with Die Events
:label: ex-die-set-operations
:class: dropdown

A die is tossed. Consider the events:
$$
A = \{2\}, \quad B = \{2, 4, 6\}, \quad C = \{1, 2\}, \quad D = \{1, 2, 4, 6\}, \quad E = \{3, 5\}
$$

Determine the events $B \cap C$, $A \cup B$, $B \cup C$, $C \cap E$, $A^c$, $B \setminus C$, $A^c \cup D$ and $A^c \cap D$.
:::

:::{exercise} Venn Diagrams
:label: ex-venn-diagrams
:class: dropdown

Given two events $A$ and $B$, use a Venn diagram to represent:

a) $A$ but not $B$
b) neither $A$ nor $B$
c) $A$ or $B$, but not both
:::

:::{exercise} Coin and Die Sample Space
:label: ex-coin-die
:class: dropdown

A coin and a die are tossed together.

a) Specify the sample space.
b) Specify the following events:
   - $A$: "heads and an even number appears"
   - $B$: "a prime number is tossed"
   - $C$: "tails and an odd number appears"
:::

### Probability measure

:::{prf:definition} Probability Measure - Axioms of Kolmogorov
:label: def-probability-measure

Consider a random experiment with sample space $\Omega$. Recall that we write $\mathcal{A}$ for the set of all possible events $E$. A probability on $\Omega$ is a function which assigns to every event $E \in \mathcal{A}$ a real number $P(E)$ and satisfies the following properties known as the **Axioms of Kolmogorov**:

A **probability measure** on $\Omega$ is a function $P : \mathcal{A} \to \mathbb{R}$ satisfying the following axioms:

**A1)** $0 \leq P(E) \leq 1$ for all events $E \in \mathcal{A}$

**A2)** $P(\Omega) = 1$

**A3)** For every sequence of mutually disjoint events $E_i$, $i = 1, 2, \ldots$ (i.e., $E_i \cap E_j = \emptyset$ for $i \neq j$), we have
$$
P\left(\bigcup_{i=1}^{\infty} E_i\right) = \sum_{i=1}^{\infty} P(E_i)
$$

We refer to $P(E)$ as the **probability** of the event $E \in \mathcal{A}$.

Events $E \in \mathcal{A}$ with $P(E) = 0$ are called **almost impossible**, events $E \in \mathcal{A}$ with $P(E) = 1$ are called **almost certain**.
:::

#### Remarks

1. **(Summation rule)** If in Axiom A3) we choose a finite sequence of disjoint events, say $E_1, E_2$ and $E_3$, we can simply set $E_i = \emptyset$ for all $i \geq 4$ to obtain
   $$
   P(E_1 \dot{\cup} E_2 \dot{\cup} E_3) = P(E_1) + P(E_2) + P(E_3)
   $$
   that is, probabilities of disjoint events sum up.

2. If the $n$ outcomes of a random experiment are equally likely to occur, then every single outcome, considered as an event, occurs with probability $1/n$. If event $A$ is the union of $k$ elementary outcomes, we have by Axiom A3),
   $$
   P(A) = \frac{k}{n} = \frac{\text{number of good outcomes}}{\text{total number of possible outcomes}} = \frac{|A|}{|\Omega|}
   $$
   We refer to such a $P$ as the **uniform probability measure** on the sample space $\Omega$.

:::{prf:example} Fair Die Probabilities
:label: ex-fair-die
:class: dropdown

In the die tossing example, if all six numbers are equally likely, we have
$$
P(\{1\}) = P(\{2\}) = P(\{3\}) = P(\{4\}) = P(\{5\}) = P(\{6\}) = \frac{1}{6}
$$

From A3) it follows that the probability of getting an even number is equal to
$$
P(\{2, 4, 6\}) = P(\{2\}) + P(\{4\}) + P(\{6\}) = \frac{1}{2}
$$
:::

We gather now some simple consequences which can be derived from the axioms of a probability measure.

:::{prf:proposition} Basic Properties of Probability Measures
:label: prop-probability-properties

Let $A, B \subseteq \Omega$ be events and $P$ a probability measure on $\Omega$. Then

- a) $P(\emptyset) = 0$
- b) $P(A^c) = 1 - P(A)$
- c) $P(A \setminus B) = P(A) - P(A \cap B)$
- d) $P(A \cup B) = P(A) + P(B) - P(A \cap B)$
- e) If $A \subseteq B$, then $P(A) \leq P(B)$
:::

:::{exercise} Prove Basic Properties
:label: ex-prove-properties
:class: dropdown

Prove of [](#prop-probability-properties):

**a) $P(\varnothing)=0$**

For a probability measure $P$ on $\Omega$, $P(\varnothing) = 0.$

The sets $\Omega$ and $\varnothing$ are disjoint and $\Omega = \Omega \cup \varnothing.$

By A3 applied to these two sets, $P(\Omega) = P(\Omega \cup \varnothing)
= P(\Omega) + P(\varnothing).$

Subtracting $P(\Omega)$ from both sides gives $0 = P(\varnothing)$

**b) $P(A^c) = 1 - P(A)$**

For every event $A \subseteq \Omega$, $P(A^{c}) = 1 - P(A).$

The sets $A$ and $A^{c}$ are disjoint and their union is the whole sample space: $\Omega = A \cup A^{c}, \qquad A \cap A^{c} = \varnothing.$

Using A3 for these two disjoint sets, $P(\Omega) = P(A \cup A^{c}) = P(A) + P(A^{c})$

By A2, $P(\Omega) = 1$, so $1 = P(A) + P(A^{c}) \quad\Rightarrow\quad P(A^{c}) = 1 - P(A)$

**c) $P(A\setminus B) = P(A) - P(A\cap B)$**
For all events $A,B \subseteq \Omega$, $P(A \setminus B) = P(A) - P(A \cap B).$

Inside $A$, split into two disjoint parts: $A = (A \setminus B) \cup (A \cap B)$, and $(A \setminus B) \cap (A \cap B) = \varnothing$.

Applying A3 to these two disjoint sets, $P(A) = P(A \setminus B) + P(A \cap B)$

Rearranging gives $P(A \setminus B) = P(A) - P(A \cap B)$

**d) $P(A\cup B) = P(A)+P(B)-P(A\cap B)$**

For all events $A,B \subseteq \Omega$, $P(A \cup B) = P(A) + P(B) - P(A \cap B)$

Decompose the union into disjoint parts: $A \cup B = (A \setminus B) \cup B$, with $(A \setminus B) \cap B = \varnothing$.

By A3, $P(A \cup B) = P(A \setminus B) + P(B)$. Using the result from (c), $P(A \setminus B) = P(A) - P(A \cap B)$ so $P(A \cup B) = \bigl(P(A) - P(A \cap B)\bigr) + P(B) = P(A) + P(B) - P(A \cap B)$.

**e) If $A\subseteq B$ then $P(A)\le P(B)$**
If $A,B \subseteq \Omega$ with $A \subseteq B$, then $P(A) \le P(B)$

If $A \subseteq B$, then $B$ can be written as the disjoint union $B = A \cup (B \setminus A)$, with $A \cap (B \setminus A) = \varnothing$.

By A3, $P(B) = P(A) + P(B \setminus A)$.

By A1, $P(B \setminus A) \ge 0$, so $P(B) \ge P(A)$, which is equivalent to $P(A) \le P(B)$.
:::

:::{prf:example} Two Fair Coins
:label: ex-two-coins
:class: dropdown

Suppose that we toss two fair coins, so that each of the four outcomes in the sample space
$$
\Omega = \{(\text{heads}, \text{tails}), (\text{heads}, \text{heads}), (\text{tails}, \text{heads}), (\text{tails}, \text{tails})\}
$$
is equally likely to occur (with probability $1/4$). Let
$$
E = \{(\text{heads}, \text{heads}), (\text{heads}, \text{tails})\} \quad \text{and} \quad F = \{(\text{heads}, \text{heads}), (\text{tails}, \text{heads})\}
$$

That is, $E$ is the event that the first coin falls heads, and $F$ is the event that the second coin falls heads. By [](#prop-probability-properties) d), we have for the probability that either the first or the second coin falls heads
$$
P(E \cup F) = P(E) + P(F) - P(E \cap F) = \frac{1}{2} + \frac{1}{2} - \frac{1}{4} = \frac{3}{4}
$$

Alternatively, since every outcome is equally likely to occur, we see directly that
$$
P(E \cup F) = P(\{(\text{heads}, \text{heads}), (\text{heads}, \text{tails}), (\text{tails}, \text{heads})\}) = \frac{3}{4}
$$
:::

:::{exercise} Unfair Die
:label: ex-unfair-die
:class: dropdown

Construct a sample space $\Omega$ and probability measure $P$ to model an unfair die in which faces $1-5$ are equally likely, but face 6 has probability $\frac{1}{3}$. Using this model, compute the probability that a toss results in a face showing an even number of dots.
:::

:::{prf:example} Probability Measure Construction
:label: ex-probability-construction
:class: dropdown

The foregoing exercise follows a typical modeling schema: First, select a suitable sample space $\Omega$, second, define $P(A)$ for all events $A$. For example if $\Omega$ is finite and all outcomes are equally likely we usually take $P(A) = \frac{|A|}{|\Omega|}$. If it is not the case that all outcomes are equally likely, then $P(A)$ would be given by some other formula.

The general situation is the following: Suppose $\Omega = \{1, 2, \ldots, M\}$ be a finite sample space. Next let $p(1), p(2), \ldots, p(M)$ be non-negative real numbers such that $\sum_{i=1}^M p(i) = 1$. For any subset $A \subseteq \Omega$, put
$$
P(A) := \sum_{i \in A} p(i)
$$

This is a well defined probability measure on $\Omega$. Analogously, one can construct a probability measure on an infinite but countable sample space.
:::

### Conditional probabilities

:::{prf:example} Two Dice Conditional Probability
:label: ex-two-dice-conditional
:class: dropdown

We toss two fair dice. Each of the 36 possible outcomes in $\Omega$ is equally likely to occur and hence has probability $\frac{1}{36}$. Now suppose that we observe that the first die is a four. Then given this information, what is the probability that the sum of the two dice equals six?

To calculate this probability we reason as follows: Given that the initial die is a four, it follows that there can be at most six possible outcomes of our experiment, namely,
$$
\Omega' = \{(4, 1), (4, 2), (4, 3), (4, 4), (4, 5), (4, 6)\}
$$

Since each of these outcomes have the same probability of occurring, they have equal probabilities. That is, given that the first die is a four, then the (conditional) probability of each of the outcomes in $\Omega'$ is $\frac{1}{6}$ while the (conditional) probability of the other 30 elements from the sample space $\Omega$ is 0. Hence the wanted probability is $\frac{1}{6}$.
:::

In general, the conditional probability is defined in the following manner:

:::{prf:definition} Conditional Probability
:label: def-conditional-probability

Let $P$ be a probability measure on $\Omega$, and let $E$ and $F$ be two events with $P(F) > 0$. The **conditional probability** of $E$ given $F$ is defined as
$$
P(E|F) := \frac{P(E \cap F)}{P(F)}
$$
:::

:::{note}
Note that $P(\cdot|F)$ is itself a probability measure in the first argument, called the **conditional probability given** $F$.
:::

:::{prf:example} Family with Two Children
:label: ex-two-children
:class: dropdown

A family has two children. What is the conditional probability that both are boys given that at least one of them is a boy?

Assume that the sample space $\Omega$ is given by $\Omega = \{(b, b), (b, g), (g, b), (g, g)\}$, all the outcomes are equally likely. ($(b, g)$ means for example that the older child is a boy and the younger a girl).

**Solution.** Letting $B$ denote the event that both children are boys, and $A$ the event that at least one of them is a boy, then the desired probability is given by
$$
P(B|A) = \frac{P(A \cap B)}{P(A)} = \frac{P(\{(b, b)\})}{P(\{(b, b), (b, g), (g, b)\})} = \frac{1}{3}
$$
:::

:::{prf:example} Drawing Balls from an Urn
:label: ex-urn-balls
:class: dropdown

Suppose an urn contains seven black and five white balls. We draw two balls from the urn without replacement. Assuming that each ball in the urn is equally likely to be drawn, what is the probability that both drawn balls are black?

**Solution.** Let $F$ and $E$ denote, respectively, the events that the first and second balls drawn are black. Now, given that the first ball selected is black, there are six remaining black balls and five white balls, and so $P(E|F) = \frac{6}{11}$. As $P(F)$ is clearly $\frac{7}{12}$, the desired probability is
$$
P(E \cap F) = P(F) P(E|F) = \frac{7}{12} \cdot \frac{6}{11} = \frac{7}{22}
$$
:::

In the preceding display, we have used that $P(E \cap F) = P(F) P(E|F)$. This rule is called **multiplication rule** and generalizes to the intersection of three (and in fact more) events:

:::{exercise} Multiplication Rule for Three Events
:label: ex-multiplication-three
:class: dropdown

Show that for any three events $A, B, C \subseteq \Omega$ such that $P(A \cap B) > 0$ we have
$$
P(A \cap B \cap C) = P(A)P(B|A)P(C|A \cap B)
$$
:::

The concept of conditional probabilities can be used to calculate probabilities in the following manner:

Let $\{A_k\}_{1 \leq k \leq n}$ be a finite partition of the sample space $\Omega$ (i.e., $\biguplus_{k=1}^n A_k = \Omega$, $A_j \cap A_i = \emptyset$ for $i \neq j$ and $P(A_j) > 0$ for every $1 \leq j \leq n$).

If $E$ is an arbitrary event, we may write
$$
E = E \cap \Omega = E \cap \left(A_1 \dot{\cup} A_2 \dot{\cup} \cdots \dot{\cup} A_n\right) = (E \cap A_1) \dot{\cup} (E \cap A_2) \dot{\cup} \cdots \dot{\cup} (E \cap A_n)
$$

If we apply the multiplication rule $n$ times, we obtain the **law of total probabilities**:

:::{prf:theorem} Law of Total Probability
:label: thm-total-probability

$$
P(E) = \sum_{k=1}^{n} P(E|A_k)P(A_k)
$$

In its most simple form, with the partition $\Omega = A \dot{\cup} A^c$, we have:
$$
P(E) = P(E|A)P(A) + P(E|A^c)P(A^c)
$$
:::

:::{prf:example} Genetic Anomaly and Stomach Cancer
:label: ex-stomach-cancer
:class: dropdown

It is suspected that stomach cancer develops with probability $p$ if some specific genetic anomaly is given. In absence of this anomaly stomach cancer develops with probability $q < p$.

Statistical estimation unveils that this anomaly is present in 0.01% of the Swiss population. Give the probability that a test person, chosen at random, has stomach cancer.

**Solution.** Let $A$ and $C$ denote, respectively, the events that the test person has the anomaly and that the test person has stomach cancer.
$$
P(C) = P(C|A)P(A) + P(C|A^c)P(A^c) = p \cdot 10^{-4} + q \cdot (1 - 10^{-4})
$$
:::

:::{warning}
Be aware that conditional probabilities behave like probabilities in the first variable but do not behave like probabilities in the second variable. In particular $P(C^c|A) = 1 - P(C|A)$, but $P(C|A) \neq 1 - P(C|A^c)$!
:::

Another useful formula is named after Thomas Bayes. This formula is applied when we have to quantify the likelihood of a hypothesis $A$ given an event $E$ (i.e., instead of $P(E|A)$ we are interested in $P(A|E)$).

A simple application of the definition of conditional probabilities followed by a formal multiplication by one yields
$$
P(A|E) = \frac{P(A \cap E)}{P(E)} \cdot \frac{P(A)}{P(A)} = \frac{P(E|A)P(A)}{P(E)}
$$

Now, if we partition $\Omega$ into the events $A$ and $A^c$ and calculate $P(E)$ using the law of total probabilities, we get **Bayes' rule**:

:::{prf:theorem} Bayes' Rule
:label: thm-bayes-rule

$$
P(A|E) = \frac{P(E|A)P(A)}{P(E)} = \frac{P(E|A)P(A)}{P(E|A)P(A) + P(E|A^c)P(A^c)}
$$
:::

:::{prf:example} Bayes' Rule Application
:label: ex-bayes-stomach-cancer
:class: dropdown

In the context of [](#ex-stomach-cancer), calculate the probability that a person with stomach cancer shows the genetic anomaly.

**Solution.** Using the same notations we have:
$$
P(A|C) = \frac{P(C|A)P(A)}{P(C|A)P(A) + P(C|A^c)P(A^c)} = \frac{p \cdot 10^{-4}}{p \cdot 10^{-4} + q \cdot (1 - 10^{-4})}
$$
:::

:::{exercise} Overloaded Cell System
:label: ex-overloaded-cell
:class: dropdown

The probability that a cell in a wireless system is overloaded is $\frac{1}{3}$. Given that it is overloaded, the probability of a blocked call is 0.3. Given that it is not overloaded, the probability of a blocked call is 0.1. Find the conditional probability that the system is overloaded given that your call is blocked.

**Answer:** 0.6
:::

:::{exercise} Autopilot Failure
:label: ex-autopilot
:class: dropdown

A certain aircraft's autopilot has conditional probability $\frac{1}{3}$ of failure given that it employs a faulty microprocessor chip. The autopilot has conditional probability $\frac{1}{10}$ of failure given that it employs a nonfaulty chip. According to the chip manufacturer, the probability that a customer receives a faulty chip is $\frac{1}{4}$. Given that an autopilot failure has occurred, find the conditional probability that a faulty chip was used.

:::{hint}
You may consider the following events:
$$
AF = \{\text{autopilot fails}\}, \quad CF = \{\text{chip is faulty}\}
$$
:::

:::{exercise} Internet Packet Routing
:label: ex-packet-routing
:class: dropdown

Due to an Internet configuration error, packets sent from Zurich to Lausanne are routed through Bellinzona with probability 3/4. Given that the packet is routed through Bellinzona, suppose it has conditional probability 1/3 of being dropped. Given that a packet is not routed through Bellinzona, suppose it has conditional probability 1/4 of being dropped.

a) Find the probability that a packet is dropped. **Answer:** 5/16
b) Can you find the conditional probability that a packet is routed through Bellinzona given it is not dropped? **Answer:** 8/11
:::

:::{prf:example} The Monty Hall Problem
:label: ex-monty-hall
:class: dropdown

In a game show, a contestant is told the rules as follows: There are three doors, labelled 1, 2, 3. A single prize is hidden behind one of them. You get to select one door. Initially your chosen door will not be opened. Instead, the gameshow host will open one of the two other doors, and he will do so in such a way as not to reveal the prize.

At this point, you will be given a fresh choice of door: you can either stick with your first choice, or you can switch to the other closed door. All the doors will then be opened and you will receive whatever is behind your final choice of door.

Imagine that the contestant chooses door 1 first; then the gameshow host opens door 3, revealing nothing behind the door, as promised. Should the contestant (a) stick with door 1, (b) switch to door 2, or (c) does it make no difference?

**Solution.** Let $H_i$ denote the hypothesis that the prize is behind door $i$, $i = 1, 2, 3$. We make the following assumptions: The three hypotheses $H_i$ are equiprobable a priori, i.e.:
$$
P(H_i) = \frac{1}{3}, \quad i = 1, 2, 3
$$

The datum we receive, after choosing door 1, is one of $D = 2$ and $D = 3$ (meaning door 2 or 3 is opened, respectively). If the prize is behind door 1 then the host has a free choice; in this case we assume that the host selects at random between $D = 2$ and $D = 3$. Otherwise the choice of the host is forced and the probabilities are 0 and 1:
$$
\begin{align}
P(D = 2|H_1) &= \frac{1}{2}, & P(D = 2|H_2) &= 0, & P(D = 2|H_3) &= 1 \\
P(D = 3|H_1) &= \frac{1}{2}, & P(D = 3|H_2) &= 1, & P(D = 3|H_3) &= 0
\end{align}
$$

Now, using Bayes' rule, we evaluate the posterior probabilities of the hypotheses:
$$
P(H_i|D = 3) = \frac{P(D = 3|H_i)P(H_i)}{P(D = 3)}
$$ {#eq-monty-hall}

Hence
$$
\begin{align}
P(H_1|D = 3) &= \frac{(1/2)(1/3)}{1/2} = \frac{1}{3} \\
P(H_2|D = 3) &= \frac{1 \cdot (1/3)}{1/2} = \frac{2}{3} \\
P(H_3|D = 3) &= \frac{0 \cdot (1/3)}{1/2} = 0
\end{align}
$$

So the contestant should switch to door 2 in order to have the biggest chance of getting the prize.
:::

:::{important} Bayesian Interpretation
Bayes' formula allows for a fruitful interpretation. Suppose that $D = \{d_1, \ldots, d_n\}$ is observed data (e.g., measurements) and $A$ a specific set of parameters (e.g., measurement conditions). Then Bayes' rule
$$
P(A|D) = \frac{P(D|A)}{P(D)} P(A)
$$
tells us how probable the parameter set $A$ is in view of the measurements $D$: One has to multiply the **likelihood** $P(D|A)$ of the observed data $D$ given the parameter set $A$ by the **a priori probability** $P(A)$ and normalize the expression by $P(D)$. The likelihood $P(D|A)$ can be viewed as a function of $A$. It expresses how probable the observed data is for different parameter sets $A$.

In view of this interpretation, Bayes' rule may be stated in words as follows:
$$
\text{posterior probability} \propto \text{likelihood} \times \text{a priori probability}
$$
where all of these terms are viewed as functions of $A$.
:::
