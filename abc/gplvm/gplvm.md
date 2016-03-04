---
title: GP - Latent Variable Model
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

## Michael Titsiasa (2009)

A Special Case of Variational Inference

Model

$$
  y = \mu(x) + \epsilon
$$

$Y$ is $N\times D$. $X$ is latent, and $N\times Q$, $Q \ll D$, that is latent variables much less than dimension of data. $p(Y|X) = \prod_{d=1}^D p(y_d|X)$, because each row in $Y$, which represents one coordinate, are independent of another. $Y=[y_1:y_2:...:y_D]$. $\kappa(x,x') = \sigma^2_f\exp\p{-\frac{1}{2} \sum_{q=1}^Q\alpha_q(x_q-x_q')^2}$. This is a GP-ARD kernel.

$p(x) = \prod_{n=1}^N N(x_n|0,I_Q)$. $p(Y,X)=p(Y|X)p(X)$.

Side Note: Sparse GP is called predictive process in machine learning.

$p(X|Y)$ is difficult to estimate. So, we estimate with

$$
  q(X) = \prod_{n=1}^N N(x_n|\mu_n,S_n)
$$

$S_n$ is a diagonal matrix. $q$ is variationally approximated posterior of $X$.

$$
\begin{aligned}
  ELBO &= \int~q(X)\log\frac{p(Y|X)p(X)}{q(X)}~dX \\
  &= \int~q(X)\log p(Y|X)~dX - \int~q(X)\log\frac{q(X)}{p(X)}~dX \\
  &= \sum_{d=1}^D\int~q(X)\log p(y_d|X)~dX - \int~q(X)\log\frac{q(X)}{p(X)}~dX \\
  &= \tilde{F}(q) - KL(q||p)
\end{aligned}
$$

Where $\tilde{F}(q) = \sum_{d=1}^D\int~q(X)\log p(y_d|X)~dX = \sum_{d=1}^D\tilde{F}_d(q)$

$$
  p(y_d,f_d,u_d | X,Z) = p(y_d|f_d) p(f_d|u_d,X,Z) p(u_d|Z)
$$

where $f_d = \mat  \mu(x_1) \\ \mu(x_2) \\ \vdots \\ \mu(x_N) \\ \tam$,
$u_d = \mat  \mu(x_1^*) \\ \mu(x_2^*) \\ \vdots \\ \mu(x_M^*) \\ \tam$,
$Z=\bc{x_1^*,...,x_M^*}$. $Z$ are knots (like in predictive process).

$$
  p(y_d|f_d) = N(y_d | f_d,\beta^{-1}I_N)
$$

where $\mat\epsilon_1\\ \vdots\\ \epsilon_N \tam \sim N(0,\beta^{-1}I_N)$.

Surface at the latent knots. Aka, predictive process:

$$
  p(f_d|u_d,X,Z) = N(f_d|K_{NM}K^{-1}_{MM}u_d,K_{NN}-K_{NM}K^{-1}_{MM}K_{MN})
$$

Finally knot GP, evaluated at knot points. Should pass through the knot points:

$$
  p(u_d|Z) = N(u_d|0,K_{MM})
$$

$p(f_d,u_d|y_d,X)$ is approximated with $q(f_d,u_d) = p(f_d|y_d,X)\phi(u_d)$.

$p(y_d|X) \ge \int\phi(u_d)\frac{ \log p(u_d) N(y_d|K_{MN}K_NN)^{-1}u_d,\beta^{-1}I_N)}{\phi(u_d)} d u_d - \frac{\beta}{2} Tr(K_{NN}-K_{NM}K^{-1}_{MM}K_{MN})$

$$
\begin{aligned}
  \tilde{F}_d(q) &\ge \int q(X)[\int\phi(u_d)\frac{ \log p(u_d) N(y_d|K_{MN}K_NN)^{-1}u_d,\beta^{-1}I_N)}{\phi(u_d)} d u_d - \frac{\beta}{2} Tr(K_{NN}-K_{NM}K^{-1}_{MM}K_{MN})] dX\\
\end{aligned}
$$

Then, change order of integrals... I'll skip the typing...

$$
\begin{array}{rcl}
  \psi_0 &=& Tr(E_{q(X)}[K_{NN}])\\
  \psi_1 &=& E_{q(X)}[K_{NM}]\\
  \psi_2 &=& E_{q(X)}[K_{MN}K_{NN}]\\
\end{array}
$$

So,...

$$
\begin{array}{rcl}
  \psi_0 &=& \sigma^2_f \prod_{q=1}^Q \frac{\exp\bc{-.5\frac{\alpha_q(\mu_{nq}-z_{mq})^2}{\alpha_q S_{nq}+1}} }{(\alpha_q S_{nq}+1)^{1/2}}\\
\end{array}
$$

Too much typing... So, just read the paper... Good luck! Variational inference is quite tedious.

The point is $\tilde{F}_d(q)$ has a lower bound. 
