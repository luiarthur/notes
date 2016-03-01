---
title: Video Lecture Summary
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

This lecture presents three popular methods of hypothesis testing and the
criticisms of each approach. There are three popular methods of hypothesis
testing

- Fisher's significance testing
- Neyman-Pearson hypothesis testing
- Jeffreys approach

In Fisherian test, a test statistic $T=t(x)$ is chosen so that large values of the statistic
indicate evidence against the null hypothesis. A p-value is computed for the test statistic
under the null model and the null is rejected when the p-value is below some predetermined value.
The p-value is the probability of observing data as or more extreme given that the null hypothesis
is true. An alternative hypothesis is not required. This methodology was developed by R. A. Fisher.

In Neyman-Pearson hypothesis testing, a pair of null and alternative hypothesis are compared. 
The null is rejected if some test statistic is larger than some predetermined critical value.
The Type I and Type II errors ($\alpha$ and $\beta$ respectively) are reported. They are respectively
the probabilities of falsely rejecting the null hypothesis and falsely accepting the null hypothesis.
This is different from the Fisherian philosophy because Neyman and Pearson *insisted* that a null
hypothesis cannot be tested alone, by needs to be accompanied by an alternative. Neyman, however, rejected 
the Fisherian philosophy because it violated the Frequentist principle.

Jeffreys uses Bayes factors (or likelihood ratio) for hypothesis testing. The bayes factor is computed as the 
ratio of the likelihoods under the null and alternative. That is

$$
  B(x) = \frac{f(x|\theta_0)}{f(x|\theta_1)}
$$

The null is rejected when $B(x)$ is less than 1, and accepted otherwise. Posterior probabilities $P(H_0|x) = \frac{B(x)}{1-B(x)}$
can be computed by assigning equal prior weights on the null and alternative hypothesis. Neither Neyman nor Fisher
approved of Jeffreys method. 

Berger gave a simple example of how the results of greatly the different methods can vary.

