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


