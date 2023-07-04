---
layout: page
title: Basic Linear Algebra
---

- [Abstract Overview](#abstract-overview)
  - [Axioms](#axioms)
  - [The Euclidean normed vector space $\\mathbb{R}^n$](#the-euclidean-normed-vector-space-mathbbrn)
  - [Linear forms and tensors](#linear-forms-and-tensors)
  - [Linear Transformations](#linear-transformations)
- [Cheat Sheet](#cheat-sheet)

## Abstract Overview

### Axioms

**Definition** A vector space $V$ over a field $F$ is an abelian group $(V,+)$ with scalar multiplication $\cdot : V \times F \rightarrow V$, which is distributive on both sides and associative.

**Corollary** $\alpha\cdot v = 0 \Rightarrow \alpha = 0 \wedge v = 0$

*Proof:* Assume $\alpha \neq 0$. Then it is invertible in $F$, and $v = (\alpha\alpha^{-1})\cdot v=\alpha^{-1}\cdot 0 = 0.\;\blacksquare$ 

**Definition** The vectors $x_1,...x_k$ are *linearly dependent* if $\exists a_1,...$ not all zero s.t. $\sum_k a_kx_k = 0$, *linearly independent* otherwise.

**Definition** The size of the largest set of linearly independent vectors is called $V$'s *dimension*.

**Theorem** Given any $n$ linearly independent vectors in an $n$-dimensional vector space $V$, every $x \in V$ has a unique representation as a linear combination of those vectors.

**Definition** For $S$, a subset of $V$, define the *span of* $S$ or $span(S)$ as the intersection of every subspace of $V$ containing $S$.

Easy to show: equivalent to saying that $span(S)$ is the smallest subspace of $V$ containing $S$ or that it contains exactly every linear combination of elements in $S$.

**Lemma** Given finite sets $S=\\{s_1,...,s_m\\}$ and $B=\\{b_1,...,b_n\\}$ s.t. $B$ is a linearly independent set of vectors in $span(S)$, $m\geq n$.

*Proof:* We proceed by induction.

Base case: since $b_1\in span(S)$, it can be represented as a linear combination of elements in $S$. We can choose an element $s_j$ which had a non-zero coefficient in this representation and rearrange to show $s_j\in span(S_1)=span(S\cup\\{b_1\\}-\\{s_j\\})$. Therefore $span(S_1)=span(S)$

$k$th case: we repeat the same procedure, choosing an $s_j$ from $S_{k-1}$ so that $S_k=S_{k-1}\cup\\{b_k\\}-\\{s_j\\}$ spans $span(S)$. Such an element of $S$ will always be removable from $S_{k-1}$, because otherwise, $b_k$ would have a representation in terms of only other elements from $B$, contradicting $B$'s linear independence. 

Now, if $m<n$, then at step $m$, $S_m\subsetneq B$. Since $span(S_k)=span(S)$ at every step, $span(S_m)\subsetneq span(B)\subset span(S_m)$, a contradiction. $\blacksquare$

**Definition** A set of linearly independent vectors $B$ in $V$ with $span(B)=V$ is called a *basis* of $V$.

**Corollary** Every basis of an $n$-dimensional vector space has $n$ elements. By considering the canonical basis, $\text{dim}(\mathbb{R}^n)=n$ follows.

**Corollary** Every linearly independent set $S$ in $V$ can be extended to a basis of $V$.  

**Corollary** Given two finite-dimensional subspaces $V$ and $W$:

$$\text{dim}(V+W)=\text{dim}(V)+\text{dim}(W)-\text{dim}(V\cap W).$$

*Proof:* Choose a basis $B$ of $span(V\cap W)$, and extend it to a basis $A$ of $V$ and a basis $C$ of $W$. Clearly $span(A\cup C)=V+W$, and its cardinality is the sum of the cardinalities of $A$ and $C$ minus that of $B$. All we need to show is linear independence.

We proceed by induction.

Base case: $A_0:=A$ is linearly independent by construction. $span(A_0)\cap span(C_0)=span(B)$ by definition, where $C_0:=C$.

$k$th case: $A_k := A_{k-1}\cup \\{c_k\\}$ and $C_k := C_{k-1} - \\{c_k\\}$. $A_k$ is linearly independent, because otherwise $c_k\in span(C_{k-1})$ but $c_k\in A_{k-1}$ which implies $c_k\in span(A_{k-1})\cap span(C_{k-1})=span(B)$, but by linear independence of $C$, $c_k\notin span(B)$, a contradiction.

To show that $span(A_k)\cap span(C_k)=span(B)$, assume otherwise. Then there exists an element of the intersection $u\notin span(B)$ such that there is a $a'\in A_{k-1}$ with $u=a'+\alpha c_k$. $\alpha$ cannot be zero, because otherwise the inductive assumption is violated. From the other side, $u=\sum^{k-1}\alpha_i c_i$, which implies

$$\sum^{k-1}\alpha_i c_i -\alpha c_k = w' \in|A_{k-1}|\cap|C_{k-1}|=|B|.$$

Which means that it has a unique representation in terms of $B$, but setting this equal to the representation in $A_k$ allows for a rearrangement that implies $span(C_k)$ is linearly dependent, which is a contradiction. $\blacksquare$

*Simpler proof:* $\alpha_i a_i + \beta_j b_j + \delta_k c_k = 0$ implies $ \alpha_i a_i = -\beta_j b_j - \delta_k c_k$, so $\alpha_i a_i\in V\cap W$, that is for some $\gamma_j$, $\alpha_i a_i -\gamma_j b_j=0$. By linear independence, $\alpha_i = 0$ for all $i$. Therefore $\beta_j b_j + \delta_k c_k = 0$, and so $b_j=c_j=0$ for all $j$. $\blacksquare$

### The Euclidean normed vector space $\mathbb{R}^n$

**Definition** The *scalar product* of two vectors $x$ and $y$ is written $x\cdot y :=\|x\| \|y\| \cos\theta$.

**Corollary** This has the following properties: 
1. $x\cdot y = y\cdot x$
2. $(\alpha x)\cdot y = \alpha (x\cdot y)$
3. $(x+y)\cdot z=x\cdot z + y\cdot z$ (Consider the canonical basis representation.)
4. $x\cdot x \geq 0$ with equality iff $x=0$

**Definition** The Kronecker delta:

$$e_i\cdot e_j = \delta_{ij}:= \begin{cases}
    1 & i = j \\
    0 & i\neq j
    \end{cases}$$

**Definition** The *cross product* of two vectors $x\times y$ is the vector $z$ such that
1. $\|z\|=\|x\|\|y\|\sin\phi$ for the angle $\phi$ between $x$ and $y$. (Area of the parallelogram)
2. $z$ is orthogonal to both $x$ and $y$.
3. $x,y,z$ form a right-handed triple.

**Definition** $(x\times y)\cdot z$ is the *scalar triple product*.

### Linear forms and tensors

TODO copy over

### Linear Transformations

TODO



## Cheat Sheet

TODO