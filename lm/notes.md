---
title: Linear Models (First Class)
geometry: margin=1in
fontsize: 12pt
header-includes: 
    - \usepackage{bm}
    - \newcommand{\norm}[1]{\left\lVert#1\right\rVert}
    - \newcommand{\p}[1]{\left(#1\right)}
    - \newcommand{\bk}[1]{\left[#1\right]}
    - \newcommand{\bc}[1]{ \{#1\} }
    - \newcommand{\abs}[1]{ \left|#1\right| }
    - \newcommand{\mat}{ \begin{pmatrix} }
    - \newcommand{\tam}{ \end{pmatrix} }
    - \newcommand{\argmin}{\text{argmin}}
---

# Resources

- [Course Website](https://ams256-spring16-01.courses.soe.ucsc.edu/)

Linear models
: $\Rightarrow$ linear in "parameters". That is 

$$
  y = f(X)\beta + \epsilon
$$

In linear models, least Squares = BLUE = MLE, for normal errors.

BLUE
: Best Linear Unbiased Estimator. $\hat\beta = (X'X)^-X'y$ are *linear* in $y$.

ANCOVA
: Analysis of Covariance. Mix of Regressions and ANOVA.

***

15 April, make-up

R: `options(contrasts=c("contr.sum","contr.poly"))`

contr.sum = the constraint that $\sum \alpha_i = 0$

Default in R for `lm(y~x)` is to set the first level parameter $\alpha_i= 0$

`lm(y ~ x - 1)` => no intercept

Estimate of $y$ is the same, though estimate of $\hat\alpha$ may be different.

LSE
: $\hat\beta = Q(\beta) = \underset{\beta}{\argmin} (y-X\beta)^T(y-X\beta)$

- find the gradient
- set the gradient = 0

Derivatives of Vectors

  - $\frac{\partial b^Ta}{\partial b} = \frac{\partial a^Tb}{\partial b} = a$
  - $\frac{\partial b^TAb}{\partial b} = (A+A^T)b$

Review: Vector Space, Subspace

Teach Span and collumn space using simple 2 by 2 examples.

Span
: The set of all linear combinations of $x_1,...,x_r \in S$  is called the space spanned by $x_1,...,x_r$. If $M$ is a subspace of $S$ and $M$ equals the space spanned by $x_1,...,x_r$ then $\bc{x_1,...,x_r}$  is called a spanning set for $M$.

column space
: In terms of $y=X\beta$. The column space of $X$ is the set of $y$'s such that there exists a $\beta$ such that $y=X\beta$.

See notes on p. 21 / 64 for the application.

Linearly Dependent: Let $x_1,...,x_r$ be vectors in $S$. If there exists scalars $\alpha_1,...,\alpha_r$ not all 0, such that $\sum \alpha_i =0_r$ then $x_1,...,x_r$ are linearly dependent. Otherwise, linearly independent.

Basis: If $M$ is a subspace of $S$ and if $\bc{x_1,...,x_r}\in S$ is a linearly independent spanning set for $M$, then $\bc{x_1,...,x_r}$ is called a basis for $M$. (check)

Rank:

Singular:

*** 

Nullspace
: $N(A) = \bc{y | Ay = 0}$. Basically the (homogeneous) solution(s) to $Ay=0$.

Rank of Column Space
: rank$C(A)$ = rank($A$)

Rank of Nullspace
: rank($N(A)$) = rows($A$) - rank($A$)

Orthonormal
:

Orthogonal Complement
: 

Figure
:

Projection
:

