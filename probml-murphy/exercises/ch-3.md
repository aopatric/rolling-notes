# Selected Exercises From Chapter 3

#### 3.1 Uncorrelated does not imply independent

Let $X \sim U(-1, 1)$ and $Y = X^2$. Clearly $Y$ is dependent on $X$ (in fact, $Y$ is uniquely determined by $X$). However, show that $\rho (X, Y) = 0$. Hint: if $X \sim U(a, b)$, then $\mathbb E[X]= (a+b)/2$ and $\mathbb V [X] = (b-a)^2/12$.

**Solution**: We can directly employ the given definition of the correlation:
$$
\rho = \frac{\text{Cov}[X, Y]}{\sqrt{\mathbb V[X] \mathbb V [Y]}}
$$
We will try to compute the covariance $\text{Cov}[X, Y] = \mathbb E[XY] - \mathbb E[X]\mathbb E[Y]$. We are given that $\mathbb E[X] = (a+b)/2 = 0$, so we can find our missing values:
$$
\mathbb E[Y] = \int_{-1}^1 x^2 \cdot 1 dx = \frac{x^3}{3}\bigr|_{-1}^{1} = \frac{1}{3} + \frac{1}{3} = \frac{2}{3}
$$
For the covariance we also need $\mathbb E[XY]$, and since $Y = X^2$, we need $\mathbb E[X^3]$:$$\mathbb E[XY] = \int_{-1}^1 x^3 dx = \frac{x^4}{4} \bigr|_{-1}^1 = 0$$Thus the covariance is given by $$\text{Cov}[X, Y] = \mathbb E [XY] - \mathbb E [X] \mathbb E[Y] = 0 - 0 \cdot \frac{2}{3} = 0$$This drives the numerator and thus the corrleation to $0$.