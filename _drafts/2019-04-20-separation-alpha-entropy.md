---
layout: post
title: Notes about the Separation $alpha$-entropy
categories: [Research, Bayesian Theory]
---

I introduced a a few weeks ago [on my retired blog](https://mathstatnotes.wordpress.com/) the notion of the *separation $\alpha$-entropy* of a set $A$ relatively to a fixed point $f_0$ and a prior distribution $\Pi$ over $\mathbb{F} \supset A$. This allowed us to formulate probable finite sample posterior concentration bounds taking the following form: for any $\delta > 0$ and $\kappa > 1$,
$$
\mathbb{P}\left(\log \Pi(A \mid \{X_i\}_{i=1}^n) \leq \frac{1-\alpha}{\alpha}\mathcal{S}^\star_\alpha(A, \delta) -\log \Pi(B(\delta, f^\star;f_0)) - n \kappa \delta \right) \geq 1-\frac{8}{\alpha^2\delta n},
$$
where $X_i \sim^{i.i.d.} f_0$, $f^\star$ is an approximation of $f_0$ inside of the model, $\mathcal{S}_\alpha$ is the separation $\alpha$-entropy of $A$ (which depends on a few things) and $-\log\Pi(B(\delta, f^\star;f_0))$ is the *local Bayesian complexity*. We also obtained general consistency results which said that, if both $\mathcal{S}_\alpha^\star(A, \delta)$ and the local Bayesian complexity are finite, then the posterior distribution almost surely concentrates in $A$ as more and more data is gathered.

The goal of this post is to discuss how we can bound $\mathcal{S}_\alpha^\star$ in finite and infinite-dimensional models, and to relate this quantity to the more well-known Hausdorff $\alpha$-entropy, metric entropies and covering numbers for testing under misspecification. 

<!--more-->

There's still a bit of work required to make things applicable to [singularly misspecified](https://mathstatnotes.wordpress.com/2019/03/26/the-misspecified-mathematical-theory-of-bayesian-misspecification/) models, but I'm keeping this for later.

### Framework

Let me restate the framework in which we work. We let $\mathcal{X}$ be a complete and separable metric space together with a $\sigma$-finite measure $\mu$ defined on its Borel $\sigma$-algebra $\mathcal{B}_{\mathcal{X}}$. We denote by $\mathbb{F}$ the set of all probability density functions on $(\mathcal{X}, \mathcal{B}_{\mathcal{X}}, \mu)$. Our basic metric structure on $\mathbb{F}$ is the Hellinger distance defined by $H(f, g) = \left(\int \left(\sqrt{f} - \sqrt{g}\right)^2\,d\mu\right)^{½}$ and we assume that the map $(f, x) \mapsto f(x)$ is jointly measurable in the product of the Borel $\sigma$-algebra.

Now let $\Pi$ be a prior on $\mathbb{F}$ and assume that we observe data $X \sim f_0 \in \mathbb{F}$. The posterior distribution is then defined (when the expression makes sense) as
$$
\Pi(A \mid X) = \int_A f(X) \,\Pi(df)\Big/ \int_{\mathbb{F}}f(X) \,\Pi(df).
$$
It may be the case that small Kullback-Leibler neighborhoods of $f_0$ are of zero prior probability. This is the *misspecified* case, in which we can shift our focus from convergence to $f_0$ to posterior concentration around approximations $f^\star$ of $f_0$ which are closer to the support of the prior (or inside the Kullback-Leibler support, or a point of minimal KL divergence in this support).

We therefore define *off-centered* divergences from $f$ to $f^\star$ with respect to $f_0$ as
$$
d_\alpha^{f_0}(f, f^\star) = -\alpha^{-1}\log A_\alpha^{f_0}(f, f^\star),
$$
where
$$
A_\alpha^{f_0}(f, f^\star) = \int_{\{f > 0\}} \left(\frac{f}{f^\star}\right)f_0 \,d\mu
$$
is the off-centered $\alpha$-affinity between from $f$ to $f^\star$. I've talked in quite some detail about these kind of divergences in the post *[Some Comparison Inequalities for Off-Centered Rényi Divergences](https://mathstatnotes.wordpress.com/2019/03/30/some-comparison-inequalities-for-off-centered-renyi-divergences/)*. When $f^\star = f_0$, we'll drop the supscript and write $d_\alpha(f, f^\star) = d_\alpha^{f^\star}(f, f^\star)$.

### The separation $\alpha$-entropy

Let $A\subset \mathbb{F}$. We say that $A$ is $\delta$-separated from $f^\star$ with respect to the divergence $d_\alpha^{f_0}$ if, for every density $f$ in the convex hull of $A$ we have that $d_\alpha^{f_0}(f, f^\star) \geq \delta$. A covering $\{A_i\}$ of $A$ is said to be $\delta$-separated from $f^\star$ with respect to $d_\alpha^{f_0}$ if every $A_i$ is $\delta$-separated from $f^\star$.

We can now define the **separation $\alpha$-entropy** of $A$ as the function of $\delta > 0$, $\Pi$, $f_0$ and $f^\star$ given by
$$
\mathcal{S}_\alpha^\star(A, \delta) = \inf \,(1-\alpha)^{-1}\log \sum_{i=1}^\infty \left(\frac{\Pi(A_i)}{\Pi(A)}\right)^\alpha
$$
where the infimum is taken over all measurable coverings $\{A_i\}$ of $A$ which are $\delta$-separated from $f_0$. When no such covering exists, we let $S_\alpha^\star(A, \delta) = \infty$ and when $\Pi(A) = 0$, we define $\mathcal{S}_\alpha^\star(A, \delta) = 0$.

I've talked about basic properties of the separation $\alpha$-entropy in [this previous post](https://mathstatnotes.wordpress.com/2019/04/08/posterior-concentration-in-terms-of-the-separation-alpha-entropy/), but now let's get to more substantive material.

## Upper bounding the separation $\alpha$-entropy by the Hausdorff $\alpha$-entropy and metric entropy

The Hausdorff $\alpha$-entropy of the prior $\Pi$ introduced by Xing (2009) is defined as
$$
\mathcal{H}_\alpha(\varepsilon) = \inf \log \sum_{i=1}^\infty \Pi(A_i)^\alpha
$$
where the infimum is taken over all coverings $\{A_i\}$ of the support of $\Pi$ which are of Hellinger diameter at most $\varepsilon$.

We can relate this global measure of prior complexity to the separation $\alpha$-entropy in the well-specified case where $f_0 = f^\star$, providing in this way global bounds on the separation $\alpha$-entropy.

**Proposition 1** (Global bounds on the separation $\alpha$-entropy).

