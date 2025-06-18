# 1: Measure Theory

Recalling important results and definitions from measure theory.

## 1.1: Probability Spaces

A **probability space** is a triple $(\Omega, \mathcal F, \mathit P)$ with $\Omega$ the set of "outcomes", $\mathcal F$ the set of "events", and $\mathit P: \mathcal F \to [0, 1]$ is a function *assigning* probabilities to events. We further assume $\mathcal F$ is a $\sigma$-algebra, i.e. it satisfies:

1. for $A \in \mathcal F$, have $A^c \in \mathcal F$ as well, i.e. the $\sigma$-algebra is *closed* under the complement
2. for $A_i \in \mathcal F$ indexed by a countable set of $i$, we find $\bigcup_i A_i \in \mathcal F$, i.e. the $\sigma$-algebra is *closed* under countable unions

It also follows that since $\bigcap_i A_i  = (\bigcup_i A_i^c)^c$, the $\sigma$-algebra is also closed under countable intersections.

If we omit the measure $\mathit P$, the tuple $(\Omega, \mathcal F)$ defines a **measurable space**,  i.e. one for which we can assign a **measure** $\mu: \mathcal F \to \mathbb R$ that is both *nonnegative* and *additive*, i.e.

1. $\mu(A) \geq \mu(\emptyset) = 0, \forall A \in \mathcal F$
2. $\mu(\cup_iA_i) = \sum_i \mu(A_i)$ 

If the total measure over all outcome space $\mu(\Omega) = 1$, then we have a special measure known as a **probability measure**.

By definition of the measure we arrive at **Theorem 1.1.1**:

For a measure $\mu$ on $(\Omega, \mathcal F)$, find:

1. monotonicity: for $A \subset B$, have $\mu(A) \leq \mu(B)$
2. subadditivity: for $A \subset \cup_{m=1}^\infty A_m$ find $\mu(A) \leq \sum_{m=1}^\infty \mu(A_m)$
3. continuity from below: if $A_i \uparrow A$, i.e. $A_1 \subset A_2 \subset \ldots$ and $\bigcup_i A_i = A$, then $\mu(A_i) \uparrow \mu(A)$
4. continuity from above: if $A_i \downarrow A$, i.e. $A_1 \supset A_2 \supset \ldots$ and $\bigcap_i A_i = A$, then $\mu(A_i) \downarrow \mu(A)$ given that $\mu(A_1) < \infty$

