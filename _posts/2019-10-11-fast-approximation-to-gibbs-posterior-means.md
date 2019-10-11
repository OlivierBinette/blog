---
layout: post
title: Early idea to approximate Gibbs posterior means
categories: [Research, Computation, Bayesian Theory]
---

Consider the statistical learning framework where we have data $X\sim Q$ for some unknown distribution $Q$, that we have a model $\Theta$ and a loss function $\ell_\theta(X)$ measuring a cost associated with fitting the data $X$ using a particular $\theta\in\Theta$. Our goal is to use the data to learn about parameters which minimize the risk $R(\theta) = \mathbb{E}[\ell_\theta(X)]$. Here are two standard examples.

**Density estimation.** Suppose we observe independent random variables $X_1, X_2, \dots, X_n$. Here the model $\Theta$ parametrizes a set $\mathcal{M} = \{p_\theta : \theta \in \Theta \}$ of probability density functions (with respect to some dominating measure on the sample space), and our loss for $X = (X_1, \dots, X_n)$ is defined as
$$
\ell_\theta(X) = - \sum_{i=1}^n \log p_\theta(X_i).
$$
If, for instance, the variables $X_i$ are independent with common distribution with density function $p_{\theta_0}$ for some $\theta_0 \in \mathbb{\Theta}$, then it follows from the positivity of the Kullback-Leibler divergence that $\theta_0 \in \arg\min _ \theta \mathbb{E}[\ell _ \theta(X)]$. That is, under identifiability conditions, our learning target is the true data-generating distribution.

If the model is misspecified, roughly meaning that there is no $\theta_0\in \Theta$ such that $p_{\theta_0}$ is a density of $X_i$, then our framework sets up the learning problem to be about the parameter $\theta_0$ which is such that $p_{\theta_0}$ mininizes the Kullback-Leibler divergence between $p_{\theta_0}$ and the true marginal distribution of the $X_i$'s.

**Regression.** Here our observations take the form $(Y_i, X_i)$, the model $\Theta$ parameterizes regression functions $f_\theta$ and we can consider a sum of squared errors loss
$$
\ell_\theta(X) = \sum_{i=1}^n(Y_i - f_\theta(X_i))^2.
$$

### Gibbs posterior distributions

**Gibbs Learning** approaches this problem from a pseudo Bayesian point of view. While typically a Bayesian approach would require the specification of a full data-generating model, here we replace the likelihood function by the *pseudo-likelihood* function $\theta \mapsto e^{-\ell_\theta(X)}$. Given a prior $\pi$ on $\Theta$, the Gibbs posterior distribution is then given by
$$
\pi(\theta \mid X) \propto e^{-\ell_\theta(X)} \pi(\theta)
$$
and satisfies
$$
\pi(\cdot \mid X) \in \text{argmin}_{\hat \pi} \left\{ \mathbb{E}_{\theta \sim \hat \pi}[\ell_\theta(X)] + D_{\text{KL}}(\hat \pi \mid \pi) \right\}
$$
whenever these expressions are well defined. 

In the context of integrable pseudo-likelihoods, the above can be re-interpreted as a regular posterior distributions built from density functions $f _ \theta(x) \propto e^{-\ell _ \theta(x)}$ and with a prior $\tilde \pi$ satisfying
$$
\frac{d\tilde \pi}{d\pi}(\theta) \propto \int e^{-\ell_\theta(x)}\,dx =: c(\theta).
$$
However, the reason we cannot apply standard asymptotic theory to the analysis of Gibbs posterior is that the quantity $c(\theta)$ will typically be sample-size dependent. That is, if $X=X^n=(X_1, X_2, \dots, X_n)$ for i.i.d. random variables $X_i$ and if the loss $\ell_\theta$ separates as the sum
$$
\ell_\theta(X) = \sum_{i=1}^nl_{\theta}(X_i),
$$
then $c(\theta) = \left(\int e^{-l_\theta(x_1)} \, dx_1\right)^n$. This data-dependent prior, tilting $\pi$ by the function $c(\theta)^n$, is what allows Gibbs learning to target general risk-minimizing parameters rather than likelihood Kullback-Leibler minimizers.

Some of my ongoing research, presented as a poster at the O'Bayes conference in Warwick last summer, focused on understand the theoretical behaviour of Gibbs posterior distributions. I studied the posterior convergence and finite sample concentration properties of Gibbs posterior distributions under the large sample regime with additive losses $\ell_\theta^{(n)}(X_1, \dots, X_n) = \sum_{i=1}^n\ell_\theta(X_i)$. I've attached the poster (joint work with Yu Luo) below and you can find the additional references [here](http://olivierbinette.ca/blog/media/2019-10-11/references.pdf).

Note that this is very preliminary work. We're still in the process of exploring interesting directions (and I have very limited time this semester with the beginning of my PhD at Duke).

![](http://olivierbinette.ca/blog/media/2019-10-11/poster.png)



### Interpolating between Empirical risk minimization and model averages

An important (both useful and somewhat annoying) feature of Gibbs posterior distributions is that they depend on the scale at which the losses are specified. That is, if considering the alternative losses $\tilde \ell_\theta(X) = \eta \ell_\theta(X)$ for some $\eta > 0$ yields a completely different Gibbs posterior distribution. As $\eta \rightarrow \infty$, we can expect the posterior distribution to converge to the empirical risk minimizer (if it exists), whereas for small $\eta$, the posterior distribution should be more vague. Choosing this scale is an open problem for which a few interesting solutions have been recently proposed.



Ok, enough background material. Let's get to the meat of this post.

# Approximating Gibbs posterior mean computation (an early idea)

I think (even though I have no precise idea yet) that there is an interesting relationship between the the choice of the scale of the loss functions previously mentionned, the process of iterating Gibbs posterior computation and the gradient descent algorithm used to compute empirical risk minimizers.

What I mean by iterating Gibbs posterior computation is the following: we start with a prior $\pi = \pi_0$, compute the posterior $\pi_1 = \pi(\cdot \mid X)$, then compute the posterior $\pi_2$ obtained by using the same data and by using $\pi_1$ as a prior, and etc. I'll refer to this as **iterated Gibbs**. I suspect (although I haven't checked anything) that this sequence $\pi_n$ converges to a point mass at the empirical risk minimizer, under some assumptions.

This idea came from a talk by Joan Bruna I attended last Wednesday at Duke. They used something similar to this iterated Gibbs method as a "proximal update" step in a gradient descent algorithm, although I'll have to look more deeply into their results to understand everything they've done (the talk was in a statistical physics framework which I'm less familiar with).

The cool thing would be if we were able to use only a few steps of iterated Gibbs, with scaled down loss functions, as an approximation to the Gibbs posterior distribution we care about. Each of these iterated Gibbs step could further be approximated by a few steps of gradient descent initialized following the relevant "prior" distributions. This could be interpreted as (very roughly) approximate Bayes while being very fast and providing some of the benefits of model averaging and incorporating prior information.



This is something I'll try to look into. I'll update this post as I either make progress or discover how this doesn't work.