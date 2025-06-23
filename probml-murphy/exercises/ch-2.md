# Selected Exercises From Chapter 2

#### 2.1: Conditional Independence
a. Let $H \in \{ 1, \ldots, K\}$ be a discrete random variable, and let $e_1$ and $e_2$ be the observed values of two other random variables $E_1$ and $E_2$. Suppose we wish to calculate the vector$$\vec{P}(H | e_1, e_2) = (P(H = 1 | e_1, e_2), \ldots, P(H=K|e_1, e_2))$$
Which of the following sets of numbers are sufficient for the calculation?

i. $P(e_1, e_2), P(H), P(e_1|H), P(e_2 | H)$

ii. $P(e_1, e_2), P(H), P(e_1, e_2 | H)$

iii. $P(e_1 | H), P(e_2 | H), P(H)$

**Solution**: We can start by cconsidering applying *Bayes' rule* to find the desired vector, which looks like:
$$
P(H| e_1, e_2) = \frac{P(e_1, e_2 | H)P(H)}{P(e_1, e_2)}
$$
We are given no further information about independence, so we can only take the set $\boxed{(ii).}$

b. Suppose we now assume $E_1 \perp E_2 | H$ (i.e., $E_1$ and $E_2$ are conditionally independent given $H$). Which of the above 3 sets are sufficient now?

**Solution**: We can re-examine the Bayes' rule application from above and use the conditional independence identity $P(e_1, e_2 | H) = P(e_1|H)P(e_2|H)$, which allows us to rewrite:
$$
\frac{P(e_1, e_2 | H)P(H)}{P(e_1, e_2)} = \frac{P(e_1|H)P(e_2|H)P(H)}{P(e_1, e_2)}
$$
Which gives us immediately that $\boxed{(i)}$ is an acceptable answer. However, we can also notice that $P(e_1, e_2)$ serves as a constant for normalization, so if we drop it from our set of information, we can replace it with a normalization constant computed afterwards:
$$
\text{recall } P(H|e_1, e_2) \propto P(e_1, e_2|H)P(H) = P(e_1|H)P(e_2|H)P(H)
$$
Showing that with the relaxation, $\boxed{(iii)}$ is now also sufficient.

#### 2.2: Pairwise Independence does not imply mutual independence

Show that pairwise independence between all pairs of variables does not necessarily imply mutual independence. It suffices to give a counter example.

**Solution**: We'll consider a problem setting of flipping two coins; we'll take two fair coins and name events $A$ and $B$ after their outcomes, (i.e., $P(A = 1) = P(B = 1) = 0.5$ for Heads $=1$) and we name a third variable as the XOR of their outcomes, i.e. $C = A \oplus B$.

We can enumerate their outcomes, and since the die are fair we can assume each outcome of $(A, B)$ occurs with probability $1/4$, giving:

| A | B | C |
| :------- | :------: | -------: |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

We can check for pairwise independence: between $A, B$ we have two independent coin tosses so they are trivially independent. We can check independence between $A, C$:
$$P(A = 0, C=0) = \frac{1}{4} \\ P(A=0) = \frac{1}{2}, P(C=0) = \frac{1}{2}\\ P(A= 0 , C= 0) = P(A = 0)P(C=0) \implies A \perp C$$

A similar argument follows for $B, C$. So The three are pairwise independent. However, we can check for mutual independence:
$$
P(A=0, B=0, C=0) = \frac{1}{4} \\
P(A=0) = P(B=0) = P(C=0) = \frac{1}{2} \\
\implies \frac{1}{4} = \frac{1}{8}
$$
Since the two are not equal, we arrive at a set of 3 variables with pairwise but not mutual independence.

#### 2.4: Convulution of two Gaussians is a Gaussian

Show that the convolution of two Gaussians is a Gaussian, i.e.,
$$
p(y) = \mathcal N(x_1 | \mu_1, \sigma^2_1) \otimes \mathcal N(x_2 | \mu_2, \sigma^2_2) = \mathcal N(y | \mu_1 + \mu_2, \sigma_1^2 + \sigma_2^2)
$$

**Solution**: We can start with the convolution formula and the PDF of the Gaussian:
$$
p(y) = \int p_1(x_1)p_2(y - x_1)dx_1 \\
p_1(x_1) = \frac{1}{\sqrt{2\pi \sigma_1^2}}\exp(-\frac{(x_1 - \mu_1)^2}{2\sigma_1^2})\\
p_2(y - x_1) = \frac{1}{\sqrt{2\pi \sigma_2^2}}\exp(-\frac{(y - x_1 - \mu_2)^2}{2\sigma_2^2})
$$
Rewriting:
$$
p(y) = \int_{-\infty}^{\infty}\frac{1}{\sqrt{2\pi\sigma_1^2}\sqrt{2\pi\sigma_2^2}}\exp(-\frac{(x_1 - \mu_1)^2}{2\sigma_1^2})\exp(-\frac{(y-x_1-\mu_2)^2}{2\sigma_2^2})dx_1 \\
= \frac{1}{2\pi \sigma_1\sigma_2} \int \exp(-E(x, y))dx_1
$$
So we can analyze the negative argument of the exponential function (we'll call it $E(x, y)$):
$$
E(x, y) = \frac{1}{2\sigma_1^2}(x_1 - \mu_1)^2 + \frac{1}{2\sigma_2^2}(x_1 - (y - \mu_2))^2 \\ = \frac{1}{2}\left[\frac{1}{\sigma_1^2}(x_1^2 - 2 x_1\mu_1 + \mu_1^2) + \frac{1}{\sigma_2^2}(x_1^2 - 2x_1(y-\mu_2) + (y-\mu_2)^2)\right] \\
= \frac{1}{2}\left[\frac{1}{\sigma_1^2}x_1^2 - \frac{2\mu_1}{\sigma_1^2}x_1 + \frac{\mu_1^2}{\sigma_1^2} + \frac{1}{\sigma_2^2} x_1^2 - \frac{2(y-\mu_2)}{\sigma_2^2}x_1 + \frac{(y-\mu_2)^2}{\sigma_2^2}\right] \\
= \frac{1}{2}\left[\left(\frac{1}{\sigma_1^2} + \frac{1}{\sigma_2^2}\right)x_1^2 - 2 \left(\frac{\mu_1}{\sigma_1^2} + \frac{(y-\mu_2)}{\sigma_2^2}\right)x_1  + \left(\frac{\mu_1^2}{\sigma_1^2} + \frac{(y-\mu_2)^2}{\sigma_2^2}\right)\right]
$$
We can use the algebraic identity
$$
ax^2 - 2bx + c = a(x - \frac{b}{a})^2 + (c - \frac{b^2}{a})
$$

TODO: continue

#### 2.6 Variance of a Sum

Show that the variance of a sum is $$\mathbb V [ X + Y ] = \mathbb V[X] + \mathbb V [Y] + 2 \text{Cov}[X, Y]$$

**Solution**: We can start by expressing
$$
\mathbb V [X + Y] = \mathbb E[(X+Y)^2] - \mathbb E[X+Y]^2 \\
= \mathbb E [X^2 + 2XY + Y^2] - (\mathbb E[X]^2 + 2 \mathbb E[X]\mathbb E[Y] + \mathbb E[Y]^2) \\
= (\mathbb E[X^2] - \mathbb E[X]^2) + 2(\mathbb E[XY] - \mathbb E[X] \mathbb E[Y]) + (\mathbb E[Y^2] - \mathbb E[Y]^2) \\
= \boxed{\mathbb V [X] + \mathbb V[Y] + 2 \text{Cov}[X, Y]}
$$
As desired.

#### 2.9 Bayes' Rule for Medical Diagnosis

After your yearly checkup, the doctor has bad news and good news. The bad news is that you tested positive for a serious disease, and that the test is 99% accurate (i.e., the probability of testing positive given that you have the disease is 0.99, as is the probability of testing negative given that you don't have the disease). The good news is that this is a rare disease, striking only one in 10,000 people. What are the chances that you actually have the disease?

**Solution**: We are given that $P(+ | \text{sick}) = 0.99$ and that $P(- | \text {healthy}) = 0.99$ . We are also given the prior that $P(sick) = 0.0001$. We want to find $P(\text{sick} | +)$. We can use Bayes' rule:
$$
P(\text {sick} | +) = \frac{P(+ | \text{sick}) P(\text{sick})}{P(+)} \\ = \frac{P(+ | \text{sick}) P(\text{sick})}{P(+ | \text{sick})P(\text{sick}) + P(+ | \text{healthy})P(\text{healthy})} \\ = \frac{0.99 \cdot 0.0001}{0.99 \cdot 0.0001 + 0.01 \cdot 0.9999} \approx 0.0098
$$
So given that we got a positive test with $99\%$  accuracy, we would expect to be sick with probability around $0.0098$.