---
title: Variational Inference
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

## Difference between ADF and VB 

1. In ADF you specify the approximating class
2. Do not specify in general

log is a concave function. Convex Eggregex. So, $E(log(X)) < log(E(X))$.

## Papers

- Jakkola & Jordan (2002), about Variational Inference for DP mixture models
- Lutz, Wand, Brooderick, Ormerod. Take all 4 combinations of three names and read those papers.

$$
\begin{aligned}
  KL(p || q) &= E_q \bk{ \log\frac{q(z)}{p(z|y)} } \\
             &= -E_q \bk{\log\p{\frac{p(z,y)}{q(z)}}} + \log p(y)\\
             &= -ELBO + \log p(y)\\
\end{aligned}
$$

So, $KL(p||q) + ELBO = \log p(y) \Rightarrow $ maximizing ELBO is equivalent to minimizing KL. 

For the Gaussian Mixtures example in the slikds,

$$
\begin{aligned}
  q(\theta_1,...,\theta_K,z_1,...,z_n) &= \prod_{k=1}^K q(\theta_k|\tilde{\mu}_k) \prod_{i=1}^n q(z_i|\phi_i) \\
  q^*(z_i) &\propto \exp\bc{E_{z_{-i}}\bk{\log p(\theta_{1:k}, z_i,z_{-i}, y_{1:n}) }} \\
  &= \log p(\theta_{1:k}) + \sum_{j\ne i} \log(p(z_j)) + \sum_{j\ne i} \log(p(y_j|z_j)) + \log p(z_i) + \log p(y_i|z_i) \\
  \Rightarrow q^*(z_i) &\propto \exp\bc{\log\pi_{z_i} + E\bk{\log p(y_i|z_i} }
  \\
  E\bk{\log p(y_i|\theta_i} &= -\frac{1}{2} \log 2\pi - \frac{y_i^2}{2} + y_i E\bk{\theta_{z_i}} - E\bk{\theta_{z_i}^2/2} \\
  \Rightarrow q^*(z_i=k) &\propto \exp\bc{\log\pi_k +  y_i E\bk{\theta_k} - E\bk{\theta_k^2/2}} \\
  \Rightarrow q^*(\theta_i) &\propto \exp\bk{E_{\theta_{-i},z_{1:n}} \bk{\log p(\theta_{1:n})} + \sum_{j=1}^n \log p(y_j|z_j) }
\end{aligned}
$$

Let the prior on $\theta_i \sim N(\lambda_1,\lambda_2)$. Then

$$
  \tilde\lambda_1 = \frac{\lambda_1 + \sum{i=1}^n E[z_i^k]y_i }{\lambda_2 + \sum_{i=1}^n E[z_i^k]}, ~~~
  \tilde\lambda_2 = \frac{1}{\lambda_2 + \sum_{i=1}^n E[z_i^k]}
$$

And $q_k^* \propto N(\theta,\tilde\lambda_1,\tilde\lambda_2)$, where $z_i^k$ is an indicator that $z_i=k$.

Solve:

$$
\begin{aligned}
  E[z_i^k] &= f_1(E[\theta_k],E[\theta_k^2]) \\
  E[\theta_k] &= f_2(E[z_i^k]) \\
\end{aligned}
$$

The point estimates are very good but very sensitive to starting values.

## Other Notes
I'm presenting on March 9 (second day)
