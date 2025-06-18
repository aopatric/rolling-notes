# 5: Algebra and (little) Calculus

### 5.1.1 Vectors
**Dot Product**

[E] What's the geometric interpretation of the dot product of two vectors?

The dot product of two vectors corresponds to the similary in their angles; a dot product of $0$ implies the vectors are orthogonal, and a maximial dot product implies the vectors are colinear. This can be seen in the expression for the dot product, namely$$a \cdot b = |a||b| \cos \theta$$

[E] Given a vector $u$, find the vector $v$ of unit length such that the dot product of $u$ and $v$ is maximum.

Since we have that the dot product should be maximum, we want a vector that is colinear. Thus our target is the unit vector in direction of $u$. Thus our target vector is in fact $$v = \frac{u}{|u|}$$

**Outer Product**

[E] Given vectors $a = [3, 2, 1]$ and $b = [-1, 0, -1]$, find the outer product $a^\top b$.

We write:
$$
a^\top b = \begin{bmatrix}3 \\ 2 \\ 1\end{bmatrix} \begin{bmatrix}-1 & 0 & -1\end{bmatrix} = \begin{bmatrix}-3 & 0 & -3 \\ -2 & 0 & -2 \\ -1 & 0 & -1\end{bmatrix}
$$

[M]$^*$ Give an example of how an outer product can be useful in ML.

The outer product comes into play when we consider things like calculating empirical covariance:
$$
\Sigma = \mathbb E[xx^\top] - \mu \mu^\top
$$
Which is formulated as the difference of two outer products.

[E] What does it mean for two vectors to be linearly independent?

In a literal sense, we say that two vectors are linearly independent iff there exists no combination of coefficients $\alpha, \beta$ other than the trivial setting such that we find $$\alpha u + \beta v = \vec{0}$$

[M] Given two sets of vectors $A = a_1, a_2, a_3, \ldots, a_n$ and $B = b_1, \ldots, b_n$, how can you check that they have the same basis?

We can consider finding $\text{rank}(A)$ and $\text{rank}(B)$ for the matrices formed with columns of the given vectors. We can then compare this to the rank of the matrix formed by joining all of the vectors $\text{rank}(A ; B)$ and if we find $$\text{rank}(A) = \text{rank}(B) = \text{rank}(A; B)$$we can conclude that they share the same basis and thus span the same subspace of dimension equal to the rank.

The reason this works is that if when we combined our matrices we got a rank higher than either of our original ranks, we know that at least one of the basis vectors for one of the matrices is not a linear combination of any of the basis vectors for the other.

[M] Given $n$ vectors, each of $d$ dimensions, what is the dimension of their span?

It depends on the linear independence relation between the vectors. An easy way to check the dimensionality of their span is to form the $d \times n$ matrix of columns given by the vectors, and find $\text{dim}(\text{span}(\{v\})) = \text{rank}(V)$.

**Norms and Metrics**

[E] What's a norm? What is $L_0, L_1, L_2, L_{norm}$?

A norm is a function $|| \cdot || : V \to [0, \infty)$ that satisfies three properties:
- nonnegativity, i.e. $||x|| \geq 0 \; \forall x \in V$
- homoegeneity, i.e. $||\alpha x|| = |a| ||x|| \; \forall x \in V$
- the triangle inequality, i.e. $||x + y|| \leq ||x|| + ||y|| $

The $\ell$ family of norms follows the formula below, with $\ell_p$ norm describing the power $p$:
$$
\ell_p(x) \triangleq \left(\sum_{i=0}^d |x_i|^p\right)^{1/p}
$$
The $\ell_0$ norm often describes the count of nonzero entries, but is not technically a norm.

[M] How do a norm and metric differ? Given a norm, make a metric. Given a metric, can we make a norm?

A metric is a function $d(x, y) : X \to \mathbb [0, \infty)$ that satisfies:
- nonnegativity, i.e. $d(x, y) \geq 0 \; \forall x, y \in X$ with $d(x, y) = 0$ iff $x=y$
- symmetry, i.e. $d(x, y) = d(y, x) \; \forall x, y, \in X$
- triangle inequality, i.e. $d(x, y) \leq d(x, z) + d(z, y)$

With this in mind, we can make a metric out of any norm; we can form
$$
d(x, y) = ||x - y||
$$
Which satisfies nonnegativity and transitivty by definition of the norm, and is symmetric because $||x - y|| = ||y-x||$. Thus we can construct a metric out of any norm. However, a metric does not have the absolute homogeneity condition that a norm does; a metric that does not hold this scaling law does not give rise to an induced norm.

#### 5.1.2 Matrices
[E] Why do we say matrices are linear transformations?

By definition, a linear transformation is a function $f: \mathbb R ^n \to \mathbb R^m$ that satisfies the following:
$$f(x+y) = f(x) + f(y) \\ f(cx) = cf(x)$$
The matrix operation matches these two properties, so it is considered a linear transformation:
$$
f(x+y) = A(x+y) = Ax + Ay = f(x) + f(y) \\
f(cx) = A(cx) = c(Ax) = cf(x)
$$

[E] What is the inverse of a matrix? Do all matrices have an inverse? Is the inverse of a matrix always unique?

The inverse of a matrix $A$ is denoted $A^{-1}$ and is also a matrix which satisfied $AA^{-1} = A^{-1}A = I$. A matrix is not always invertible, and invertibilty can be checked by ensuring the determinant is nonzero. The inverse of a matrix, if it exists, is unique.

[E] What does the determinant of a matrix represent?

The determinant, geometrically, represents the scaling factor. If we consider the unit n-cube to be composed of the space between the unit vectors, then the volume (area, length, etc.) of the unit n-cube after the trasnformation is the value of the determinant. When the determinant is negative, it can be interpreted as a sort of reflection.

[E] What happens to the determinant of a matrix if we multiply one of its rows by a scalar $t \times R$?

The determinant is *linear* in each row of the matrix, so scaling a row will also scale the determinant by that amount.

[M] A 4x4 matrix has four eigenvalues $3, 3, 2, -1$. What can we say about the trace and the determinant of this matrix?

Its trace is $3 + 3 + 2 -1 = 7$ since it is the *sum* of the eigenvalues, and the determinant is $3 * 3 * 2 * -1 = -18$ since the determinant is the *product* of the eigenvalues.

[M] Given the following matrix:

$$\begin{bmatrix}1 & 4 & -2 \\ -1 & 3 & 2 \\ 3 & 5 & -6\end{bmatrix}$$
Without explicitly using the equation for calculating determinants, what can we say about this matrix's determinant?

We can immediately notice that columns 1 and 3 are linearly dependent, with column 3 being $-2$ times column 1. Since the matrix is not full rank, it is singular and thus has a determinant of $0$.

[M] What's the difference between the covariance matrix $A^\top A$ and the Gram matrix $AA^\top$?

The covariance matrix measures the linear correlation (via dot product) of the columns in $A$, and the Gram matrix can be interpreted as doing the same operation but on the rows of $A$; if the rows were data samples, then this Gram matrix can also be interpreted as covariance.

