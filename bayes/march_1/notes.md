---
title: Notes for Bayesian class 1 March
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

$|z|$ p-values: $P(H_0|x)$

|---|---|---|
| n | 1.96 (.05) | 2.576 (.01) |
|1 |.35 |.21 |
|10 |.37 |.24 |
|100 |.60 |.27 |
|1000 |.8 |.53 |

## Model Comparison

For models $M_1,...,M_M$

$$
  P(M_i|x) = \displaystyle \frac{p(x|M_i)P(M_i)}{\sum_{j=1}^m p(x|M_j)P(M_j)}
$$

where $p(x|M_i) = \int~p(x|\theta_i;M_i)\pi(\theta_i|M_i) ~d\theta_i$


**Issues with Bayes Factors**

- Not well defined when an improper prior is used
- Proper but "vauge"


**Other Model Selection Criteria**

- BIC: Bayesian Information Criterion = $-2 \log(L(\hat\theta|x)) + p\log(n)$, where $p$ is the number of parameters and $L(\hat\theta|x))$ is the maximized likelihood.
- AIC: Akaike's Information Criterion = $-2 \log(L(\hat\theta|x)) + 2p$, where $p$ is the number of parameters and $L(\hat\theta|x))$ is the maximized likelihood.

AIC tends to overestimate number of parameters, BIC tends to underestimate the number of parameters. One challenge in computing AIC and BIC is that the number of parameters is not easy to count in hierarchical settings.

