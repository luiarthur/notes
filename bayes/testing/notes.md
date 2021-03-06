---
title: More on Hypothesis Testing
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

BIC = $-2 \log(L(\hat\theta)) + p\log(n)$
AIC = $-2 \log(L(\hat\theta)) + 2p$

We want BIC,AIC to be small.

Compare $M_1,M_2$. 

$$
  S = -.5[BIC(M_1)-BIC(M_2)]
$$

We can show that $-2S = -2\log(BF(M_1,M_2))$.


## Bayes Factors: Computation

- Using Laplace approx
- Using posterior samples 

### Laplace Approximation

$$
\begin{aligned}
  p(x|H_i)&=\int p_i(x|\theta_i)\pi_i(\theta_i|H_i)d\theta_i
  &= \int \exp\p{-n\bc{-\frac{1}{n}\log p_i(x|\theta_,H_i) -\frac{1}{n} \log\pi_i(\theta_i|H_i) }} d\theta_i,
\end{aligned}
$$

where $H_i$ can be a model.

$$
  BF(H_0,H_1) \approx (2n\pi)^{(p_0-p_1)/2} \frac{p_0(x|\hat\theta_0)\pi(\hat\theta_0)} {p_1(x|\hat\theta_1)\pi(\hat\theta_1)} \sqrt{\frac{\Sigma_0}{\Sigma_1}}
$$


$$
\begin{aligned}
  p(x|H_i)&=\int p_i(x|\theta_i)\pi_i(\theta_i|H_i)d\theta_i\\
  \theta_i^{(1)},...,\theta_i^{(M)} &\sim \pi_i(\theta_i|H_i)\\
  \hat p (x|H_i) &= \sum_{i=1}^M p_i(x|\theta_i^{(m)},H_i) / M
\end{aligned}
$$

If we have posterior samples, and dim($\theta_1$) = dim($\theta_0$)
$$
\begin{aligned}
  BF(M_0,M_1) &= \sum_{i=1}^M \frac{p_0(x|\theta^{(m)},M_0)\pi_0(\theta^{(m)})}{p_1(x|\theta^{(m)},M_1)\pi_1(\theta^{(m)})} / M
\end{aligned}
$$


Case II: Nested (dimension of parameters not the same)

Example:
$$
\begin{array}{rcl}
  M0: & y_i&= \beta_0 + \beta_1 x_i + \epsilon_i\\
  M1: & y_i&= \beta_0^* + \beta_1^* x_i + \beta_2^* z_i+ \epsilon_i
\end{array}
$$

Int this case it is also possible to obtain an approximation to the BF using
samples from the posterior distribution of $M_1$. The approximation will have
the form

$$
  \sum_{m=1}^M r(\theta^{(m)})
$$

Exercise: find $r(\theta^{(m)})$

## Hierarchical Models

Putting priors on parameters.
