---
title: Hypothesis Testing
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

## Classical Setting

$H_0: \theta \in \Theta_0$ vs. $H_1: \theta \in \Theta_1$

|---------------------|:-------------:|:---:|
|                     |$H_0$ is True   |$H_0$ is False|
|Reject $H_0$         |Type I error |Correct 
|Fail to Reject $H_0$ |Correct      |Type II error 

## Decision Theoretic Approach

$$
  L(\theta,\delta) = \begin{cases}
    \delta,  & \text{if } \theta \in \Theta_0 \\
    1-\delta,& \text{if } \theta \in \Theta_1
  \end{cases}
$$

for $\delta = \{0,1\}$.

Risk: 

### Frequentist Version

$$
  R(\theta,\delta) = \int~L(\theta,\delta(x)) f(x|\theta)~dx
$$

$$
  \begin{cases}
    P(\delta(x)=1) & \theta\in\Theta_0  \text{ Type I error} \\
    P(\delta(x)=0) & \theta\in\Theta_1  \text{ Type II error}
  \end{cases}
$$

### Bayesian Version

$$
  \int ~ L(\theta,\delta(x)) \pi(\theta|x) ~ dx = \begin{cases}
    \pi(\theta\in\Theta_1|x), & \delta=0 ~ \text{ (Don't reject) }\\
    \pi(\theta\in\Theta_0|x), & \delta=1 ~ \text{ (reject) }
  \end{cases}
$$

## Bayes Factors

The posterior odds ratio is given by 

$$
  \frac{p(\Theta_0|x)}{p(\Theta_1|x)} = \frac{p(x|H_0)}{p(x|H_1)} \frac{p(H_0)}{p(H_1)}
$$

The factor $B_{01} = \frac{p(x|H_0)}{p(x|H_1)}$ updates the prior odds ratio to the posterior odds ratio. This is known as the Bayes Factor in favr of $H_0$.

When $H_0$ and $H_1$ are both simple hypotheses, the BF corresponds to the likelihood ratio $B_{01}=\frac{p(x|\theta_0)}{p(x|\theta_1)}$. In general, if $g_i(\theta)$ is the prior for $\theta$ under $H_i$, then

$$
  B_{01} = \frac{\int_{\Theta_0}~p(x|\theta)g_0(\theta)~d\theta}{\int_{\Theta_1}~p(x|\theta)g_1(\theta)~d\theta} = \frac{m_0(x)}{m_1(x)}
$$

|:---:|:---:|:---:|
|$\log_{10} BF(H_1,H_0)$|$BF(H_1,H_0)$|Evidence against $H_0$|
|---|---|---|
|0-.5|1-3.2|Not work more that mentioning|
|.5-1|3.2-10|Substantial|
|1-2|10-100|strong|
|$> 2$|$> 100$|Decisive|

Bayes factors cannot be reconciled with the p-values in two-sided tests.

$B_{ij}(x) = \frac{m_i(x)}{m_j(x)}$, $p(M_k|x) = \p{\sum_{i=1}^m \frac{p(M_i)}{p(M_k)}B_{jk}}^{-1}$,
$m_k(x) = \int_{\Theta_k}~p_k(x|\theta_k)p_k(\theta_k)~d\theta_k$

If the priors $p_k(\theta_k)$ are defined up to a proportionality constant $c_k$, then the BF will depend on the ratio of such constants. If the priors are proper densities, then we have

$$
  c_k^{-1} = \int_{\Theta_k} p_k(\theta_k)d\theta_k
$$

and then the BF is uniquely defined. For improper priors, not defined.
