---
title: GP based models for big N
geometry: margin=1in
fontsize: 12pt
header-includes: 
    - \usepackage{bm}
        
---

\newcommand{\norm}[1]{\left\lVert#1\right\rVert}

$$
  y = \mu_0(x) + \epsilon, \epsilon \sim N(0,\sigma^2)
$$
where $\mu$ is an unknown function of the covaraites.

Prior on a function is a stochastic process.

$\mu \sim GP(m(\cdot),\kappa(\cdot,\cdot))$ where $m(\cdot)$ is a known function to center the GP. In many applications, $m(\cdot)=0$ . Covariance kernel is a function that specifies covariance between $\mu(x)$ and $\mu(z)$. $cov(\mu(x),\mu(z) = \kappa(x,z)$.

Covariance kernel determines smoothness of the prior realizations. Holder $\alpha$-continuous continuous.

If $\kappa(x,z) = \kappa(||x-z||)$ then the kernel is stationary. That is if the covariance depends only on the distance, it is stationary.

### Popular kernel choices

- exponential kernel: $\tau^2\exp(-\phi||x-z||)$
- squared exponential / Gaussian kernel: $\tau^2\exp(-\phi||x-z||^2)$
- matern function: $\frac{\tau^2(\phi||x-z||)^\nu}{\Gamma(\nu)2^{\nu-1}}\kappa_\nu(\phi||x-z||)$ where $\kappa_\nu$ is the modified Bessel function of the second kind.
    - $\nu$: smoothness parameter
        - $\nu=1/2 \Rightarrow$ exponential kernel
        - $\nu=\infty \Rightarrow$ Gaussian kernel
        - The realizations of Gaussian process with matern kernel is the floor of $\nu$ times continuity differentiable.
    - $\phi$: range / decay parameter
    - $\tau^2$: spatial variability

Hao Zhange (2004) proved that $(\tau^2,\phi,\nu)$ cannot be consistently estimated together. But a function of the parameters $\tau^2\phi^{2\nu}$ can be estimated. You need two of the three parameters to estimate the other. Fix $\nu$ and estimate $\phi$ and $\tau^2$. $\phi \sim U(a,b)$ using empirical variogram.
$$
\begin{aligned}
  \mu(.) &\sim GP(0,\kappa(.,.,\theta)) \\
  \mu(x) &\sim MVN(0,K) \\
\end{aligned}
$$

where $K_{ij} = \kappa(x_i,x_j,\theta)$. So 

$$
\begin{aligned}
  y &= \mu + \epsilon \\
  &\epsilon \sim N(0,\sigma^2I)\\
  &\mu \sim N(0,K)\\
  &N(y|0,\sigma^2I+K)
\end{aligned}
$$

In MCMC, the posterior for the hyperparameters will involve matrix inversion of $n\times n$ matrices in the likelihood.

### Research

1. low rank models
    - Sherman-Woodbury-Morrison Matrix Identity. Look it up. Use it for inverting $\sigma^2I + K$. Reduces $n^3$ to $n^2$.
2. class of sparsity based models
