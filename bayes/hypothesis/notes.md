---
title: Woodbury for GP
geometry: margin=1in
fontsize: 12pt
header-includes: 
    - \usepackage{bm}
    - \newcommand{\norm}[1]{\left\lVert#1\right\rVert}
    - \newcommand{\p}[1]{\left(#1\right)}
    - \newcommand{\bk}[1]{\left[#1\right]}
    - \newcommand{\bc}[1]{ \{#1\} }
    - \newcommand{\abs}[1]{ \left|#1\right| }
---

$$
\begin{aligned}
  y|\mu, \sigma^2 &\sim N(\mu(x), \sigma^2I) \\
  \mu &\sim N(0, K) \\
  \Rightarrow\\
  \pi(\centerdot | y) &\propto N(y | 0, \sigma^2I+K)
\end{aligned}
$$

For matrix inversion of $\sigma^2I+K$ there are two ways to solve

1. Low rank methods
2. Sparsity based methods

## Low rank methods

  - Kernel convolution (Higdon 2001)
      - $\mu(x) \int~\kappa(x-u)z(u)~du$
      - if $\mu(x)$ is a Gaussian it can be written in the above way where $\kappa(\cdot)$ is some function and $z(u)$ is a white noise process.
      - $\mu(x) \approx \sum_{l=1}^m \kappa(x-u^*_l) z(u^*_l)$, $u_l^*$ are $p\times 1$
      - $y_i = \sum_{l=1}^m \kappa(x-u_l^*)z(u_l^*) + \epsilon_i$ becomes the new fitted model instead of the original $y_i = \mu(x_i) + \epsilon_i$
$$
\begin{pmatrix}
  y_1 \\
  \vdots\\
  y_n
\end{pmatrix}
=
\begin{pmatrix}
  \kappa(x_1-u_1^*) & \cdots &\kappa(x_1-u_m^*)\\
  \vdots & & \vdots\\
  \kappa(x_n-u_1^*) & \cdots &\kappa(x_n-u_m^*)\\
\end{pmatrix}
\begin{pmatrix}
  z(u_1^*)\\
  \vdots\\
  z(u_m^*)\\
\end{pmatrix} +
\begin{pmatrix}
  \epsilon_1\\
  \vdots\\
  \epsilon_n
\end{pmatrix}
$$

$\Rightarrow y = Mz + \epsilon$, $\epsilon \sim N(0,\sigma^2I)$, $z\sim N(0,\sigma^2I)$

$$
\begin{aligned}
 \pi(-|y) & \propto & N(y|Mz,\sigma^2I) \times N(z|\sigma^2I) \times \pi(-) \\
 \pi(-|y) &\propto & N(y|0,M\Sigma M'+\sigma^2I) \times \pi(-)
\end{aligned}
$$

We need to evaluate $N(y|0,M\Sigma M'+\sigma^2I)$ every mcmc iteration. 
So, 
$$
  (M\Sigma M' + \sigma^2I)^{-1} = \frac{1}{\sigma^2}I - \frac{M}{\sigma^2} (\frac{1}{\sigma_z^2}I+\frac{M'M}{\sigma^2})^{-1} \frac{M'}{\sigma^2}
$$
if $m$ (number of knots) is small, poor approximation; $m$ is large then computational issues occur. Choice of kernel $\kappa$ is arbitrary.
$u$ are the know points. They can be an equispacing grid points of the spatial map. Random knots work too. $m$ is the number of knots.

$$
  y = \sum_l^L \kappa_l z_l + \epsilon
$$

$\kappa_l = \kappa(x-u_l^*)$ but we do not known which $\kappa$ to use. Sometimes, wavelet based functions.


## Gaussian Predictive Process Model (Bauerjee, Gelfand, Finley & Sang, JRSS-B, 2008)

- knots: $s^* = s_1^*, ..., s_m^*$
- $w(s)$: the GP to fit to the data
- Goal is to fit $y=\mu(s)+\epsilon$, $\mu \sim GP(0,\kappa(.,.))$
- Fit instead $y = \tilde\mu(s) + \epsilon$ where $\tilde\mu(s) = E[\mu(s) | \mu(s_1^*),..\mu(s_m^*)]$

$$
\begin{pmatrix}
  \mu(s)\\
  \mu(s_1^*)\\
  \vdots\\
  \mu(s_m^*)\\
\end{pmatrix} \sim N(0,G)
$$

Where $G$ is 
$$
\begin{pmatrix}
  \tau^2 & C \\
  C' & K^*
\end{pmatrix}
$$

So, $E[\mu(s) | \mu(s_1^*),..\mu(s_m^*)]  =  0 + C (K^*)^{-1} \mu(s^*)$

if $C(K^*)^{-1}$ is the basis function and $\mu(s^*)$ is the basis coefficients, then
$$
  \begin{aligned}
    y &= \tilde\mu(s) + \epsilon \\
    &= C(s) (K^*)^{-1} \mu(s^*) + \epsilon \\
    &= H\mu(s^*) + \epsilon
  \end{aligned}
$$
where, $\epsilon \sim N(0,\sigma^2I)$

Now, 
$$
  \pi(-|y) \propto N(y | H\mu(s^*), \sigma^2I) \times N(\mu(s^*)|0,K^*) \times \pi(-)
  \pi(-|y) \propto N(y | 0, \sigma^2I + HK^*H') \times \pi(-)
$$
The second line is obtained by integrating out $\mu(s^*)$.

Now we can use woodbury to invert the covariance matrix
$$
  (\sigma^2I + HK^*H')^{-1} = \frac{1}{\sigma^2}I - \frac{H}{\sigma^2} \p{(K^*)^{-1}+\frac{H'H}{\sigma^2}}^{-1} \frac{H'}{\sigma^2}
$$

$n = 10000, m = 500-600$


## Sparsity based methods

The problem once again is inverting $G=(\sigma^2I+K)$ which is $n\times n$. This is $O(n^3)$. If we can strategically make $G$ sparse, we can invert the matrix in much less time.