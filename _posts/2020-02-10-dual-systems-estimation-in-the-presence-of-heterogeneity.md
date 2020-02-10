---
layout: post
title: Dual systems estimation in the presence of heterogeneity.
categories: [Capture-Recapture, Multiple Systems Estimation, Misc]
---

*I show how the Lincoln-Petersen estimator for dual systems estimation is an upper-bound (resp. lower-bound) estimator when there is negative (resp. positive) dependency between samples).* 

Dual systems estimation (or the capture-recapture census) refers to a set of methods used to estimate the size of a given population when exhaustive enumeration is infeasible. The overlapping pattern of two random samples is used to estimate the proportion of missed (unobserved) individuals and therefore to obtain a population size estimate.

To formalize the idea, we label the individuals of this population by the integers $1,2, 3, \dots, N$, where $N$ is the unknown population size. We are given two random samples $\ell_1, \ell_2 \subset \{1,2,\dots, N\}$ and, at the risk of having to relabel the individuals, we can assume that the first $n$ of them are observed. That is, we write $\ell_1 \cup \ell_2 = \{1,2,\dots, n\}$. The Lincoln-Petersen estimator is then given by

$$
\hat N = \frac{|\ell_1||\ell_2|}{|\ell_1 \cap \ell_2|}.
$$

It relies on the assumption that $\ell_1$ and $\ell_2$ are independent samples from the population, and it is also typically assumed that the probabilites that individuals appear on a given list are constant across individuals.

Now let $X_i = (X_{i,1}, X_{i,2})$, where $X_{i,j} = 1$ if individual $i$ appears on the $j$th sample and $X_{i,j} = 0$ otherwise. We denote by $p_i$ the probability mass function of $X_i$, that is $p_i(x) = \mathbb{P}(X_i = x)$ for $x \in \{0,1\}^2$, and we assume individual-level independence of the samples, meaning that $p_i(x) = \prod_{j=1}^2 p_{i,j}^{x_j} (1-p_{i,j})^{1-x_j}$ for given probabilities $p_{i,j}$. Heterogeneity is introduced both across individuals and across lists through the model

$$
X_i \mid \{p_i\}_{i=1}^n \sim p_i,\\
\{(p_{i,1}, p_{i,2})\}_{i=1}^n \sim^{i.i.d.} \lambda.
$$

The marginal distributions of $p_{i,1}$ and $p_{i,2}$ represent individual heterogeneity, while dependency between these capture probabilities represent list dependency. More precisely, let $p_1 = \mathbb{E}[p_{i,1}]$, $p_2 = \mathbb{E}[p_{i,2}]$ and let

$$
\rho = \text{Cov}(p_{i,1}, p_{i,2}).
$$

We show here that, if $\rho > 0$ (positive dependency between the lists), then $\hat N$ estimates a *lower bound* of $N$, in a way to be precised. If $\rho <0$, then $\hat N$ estimates an *upper bound* of $N$. Furthermore, in the large-system limit of $N \rightarrow \infty$, this translates to a relative bias of $\hat N$ which we can precisely quantify through the hidden figure $\eta_0$, the number of unseen individuals, as

$$
\frac{\hat \eta_0}{\eta_0} \rightarrow r(\rho, a, b) := \frac{\rho^2 + (a+b)\rho + ab}{\rho^2 - (1-a-b)\rho + ab}, \quad a = p_1p_2,\quad b = (1-p_1)(1-p_2).
$$

Furthermore, $\rho > 0 \Rightarrow r(\rho, a, b) > 1$ and $\rho < 0 \Rightarrow r(\rho, a, b) < 1$. 

These results formalize the well-known behaviour of the Lincoln-Petersen estimator in the presence of list dependency. The ideas have also been presented in [Chao (2018)](https://www.ncbi.nlm.nih.gov/pubmed/19067330), but my exposition is a bit different.

For the proof, first note that for $x \in \{0,1\}^2$,

$$
p(x) := \mathbb{E}[p_i(x)] = \prod_{j=1}^2 p_{j}^{x_j}(1-p_j)^{1-x_j} + (-1)^{x_1x_2}\text{Cov}(p_{i,1}, p_{i,2}).
$$

Writing $n _ x = \# \{i: X _ i = x\} $ for the number of individuals with capture pattern $x$ and $\eta _ x = \mathbb{E}[n _ x]$, we also find $\eta _ x = N p(x)$ and therefore, by the above,

$$
\frac{\eta_{(0,0)}\eta_{(1,1)}}{\eta_{(1,0)}\eta_{(0,1)}} = \frac{\left( (1-p_1)(1-p_2) + \rho\right)\left( p_1p_2  + \rho\right)}{\left( p_1(1-p_2) - \rho\right)\left( (1-p_1)p_2 - \rho\right)} = r(\rho, a, b).
$$

Since the Lincoln-Petersen corresponds to

$$
\hat \eta_{(0,0)} = \frac{n_{(0,1)} n_{(1,0)}}{n_{(1,1)}}
$$

and since $\hat \eta_{(0,0)} \sim \frac{\eta_{(0,1)} \eta_{(1,0)}}{\eta_{(1,1)}} = \frac{\eta_{(0,0)}}{r(\rho, a, b)}$, we obtain the stated results.

**Remark:** the (large system) relative bias of the Lincoln-Petersen estimator only depends on capture heterogeneity through the covariance $\rho$: heterogeneity only matters in this way if it is correlated across lists.

