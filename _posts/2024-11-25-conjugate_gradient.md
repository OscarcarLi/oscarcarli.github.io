---
title: "Conjugate gradient"
author_profile: false
read_time: false
share: false
related: false
classes: wide
permalink: /CG/
published: false
---

In this post, we'll look at the conjugate gradient algorithm for solving $Ax = b$, with $A \in \mathbb{S}^{n}_{++}$ (an $n \times n$ symmetric, positive definte matrix), and $x, b \in \mathbb{R}^n$.

To understand the algorithm, we first review orthogonal basis in an inner product space.

### Inner product space and orthogonal decomposition

Given a vector space $V$ over the reals $\mathbb{R}$, an inner product over $V$ is a function $\langle\; \cdot\;, \; \cdot \; \rangle: V \times V \rightarrow \mathbb{R}$, with the properties:

- $\langle u, v \rangle = \langle v, u \rangle$ for $u, v \in V$ (symmetry)
- $\langle au + bv, w \rangle = a\langle u, w \rangle + b\langle v, w \rangle$, for $u, v, w \in V$, $a, b \in \mathbb{R}$. (linearity)
- $\langle v, v \rangle \ge 0$ for all $v \in V$ and $\langle v, v \rangle = 0$ iff $v = \mathbf{0}$. (positive definiteness)

_Definition_. $u, v \in V$ are _orthogonal_ with respect to inner product $\langle \cdot, \cdot \rangle$, if $\langle u, v \rangle = 0$.

_Theorem_: For a finite dimensional vector space of $$V$$ with $\mathrm{dim}(V) = n$ associated with inner product $\langle \cdot, \cdot \rangle$, there exists an orthogonal basis $p_1, p_2, \ldots, p_n$. This basis can be constructed through the gradient schmidt process by using the __Gram Schmidt__ process.

With an orthogonal basis $p_1, p_2, \ldots, p_n$, we can express any $x \in V$ through the projection onto individual basis vector:

\\[x = \sum_{i=1}^n \frac{\langle x, p_i \rangle}{\langle p_i, p_i \rangle} p_i.\\]

#### Examples of inner product space
For any positive definite matrix $A \in \mathbb{S}^{n}_{++}$, we can define an inner product $\langle \cdot, \cdot \rangle_A$ with $\newcommand{\coloneqq}{\mathrel{:=}}
 \langle u, v \rangle_A \coloneqq u^\top A v$. We can check that it satifies all three properties required of an inner product. By having $$A = I_{n \times n}$$, we recover the standard Euclidean inner product $u^\top v$.


### Projecting the solution $x^\star$ to $Ax = b$.
Suppose we are given an orthogonal basis of $p_1, p_2, \ldots, p_n$ for $\mathbb{R}^n$ under the inner product $\langle \cdot, \cdot \rangle_A$ (for now we ignore how we obtain such a basis), then we can express the solution $x^\star$ to $Ax = b$ using the equation above:

$$\begin{align} x^\star =& \sum_{i=1}^n \frac{\langle x^\star, p_i \rangle_A}{\langle p_i, p_i \rangle_A} p_i \nonumber \\
=& \sum_{i=1}^n \frac{p_i^\top A x^\star}{\langle p_i, p_i \rangle_A} p_i \nonumber \\
=& \sum_{i=1}^n \frac{p_i^\top b}{\langle p_i, p_i \rangle_A} p_i \label{eqn:x_projection}
\end{align}$$

Based on Equation \eqref{eqn:x_projection}, we have found a way to find $x^\star$ if we know what the orthogonal basis is, which we now turn to.

### Finding a good orthogonal basis