---
layout: post
title: Some bounds on the Jensen functional
categories: [Proof techniques, Misc]
---

Given convex  function $\varphi : \mathbb{R} \rightarrow \mathbb{R}$ and $X$ a random variable on $\mathbb{R}$ (both integrable), the Jensen functional of $\varphi$ and $X$ is defined as
$$
\mathcal{J}(\varphi, X) = \mathbb{E}[\varphi(X)] -\varphi(\mathbb{E}[X]).
$$
The well-known Jensen inequality states that $\mathcal{J}(\varphi, X) \geq 0$. 

Now write $\mu = \mathbb{E}[X] $. If $X$ is bounded, then a converse to the Jensen inquality can be easily obtained as follows: let $m$ and $M$ be the infimum and maximum of $X$, and write $X = \alpha m + (1-\alpha)M$ for some random variable $\alpha$ taking values in $[0,1]$. Then $\mathbb{E}[\alpha] = (M - \mu)/(M-m)$ and consequently
$$
\mathcal{J}(\varphi, X) \leq \mathbb{E}[\alpha\phi(m) + (1-\alpha)\phi(M)] - \varphi(\mu) = \frac{(M-\mu)\varphi(m) + (\mu-m)\varphi(M)}{M-m}- \varphi(\mu).
$$
When $\mu$ is unknown in practice, then maximizing the above over all possibilities yields
$$
\mathcal{J}(\varphi, X) \leq \max_{p \in [0,1]} \left\{p\varphi(m) + (1-p)\varphi(M) - \varphi(pm + (1-p) M)\right\}
$$
which is Theorem C in [Simic (2011)](https://www.sciencedirect.com/science/article/abs/pii/S0096300309007346).

## Examples

**Variance bound.** Consider for example the case where $\varphi(x) = x^2$, so that $\mathcal{J}(\varphi, X) = \text{Var}(X)$. <!--more-->Then for $X$ taking values in say $[0,1]$, the above bounds read as
$$
\text{Var}(X) \leq \mu(1-\mu) \leq 1/4
$$
which is a well-known elementary result. 

**$f$-divergence bounds.** In [(Binette, 2019)](https://arxiv.org/abs/1805.05135), I show how we can use similar ideas to get best-possible upper bounds on $f$-divergences in terms of the total variation distance and likelihood ratio extremums. In particular, with $D(\mu\|\nu) = \int \log\left(\frac{d\mu}{d\nu}\right) d\mu$ the Kullback-Leibler divergence between the probability measures $\mu$ and $\nu$, we find that if $a = \inf \frac{d\nu}{d\mu}$ and $b = \sup \frac{d\nu}{d\mu}$, then                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  
$$
D(\mu|\nu) \leq \sup_A|\mu(A) - \nu(A)| \left(\frac{\log(a)}{a-1} +\frac{\log(b)}{1-b}\right).
$$

## Variations on these Jensen functional bounds



## Bounds based on Laplace approximations











