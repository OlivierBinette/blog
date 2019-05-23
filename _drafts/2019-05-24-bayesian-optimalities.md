---
layout: post
title: Bayesian Optimalities
categories: [Bayesian Theory]
---

I'm sometimes asked in conferences and meetings around Montreal: *why Bayes?* 

This always strikes me. I do sometimes identify with "bayesianism", because I want to do research related to Bayesian statistics, but I don't feel that I'm a Bayesian in the sense that I adhere to one particular school of thought. First and foremost, I am a mathematician and a statistician. I want to understand the world through simulation and modelling, with the certainty provided by mathematical lenses, and I want to study and develop the statistical tools that we use to understand the world when certainty is not at reach. That's my scientific identity.

Yet I'm also driven to answer: *what else?* What else than probabilities to model uncertainty and randomness? What else than probabilistic conditioning to account for new information? (Ok, I'm exaggerating a bit here. There are tons of other fun "else" to answer that question, but Bayes certainly stands out.) I'm drawn to Bayesian stats because, more often than not, it's about providing meaningful answers to the questions that we really care about. I want, when possible, posterior probabilities of hypotheses; not 0-1 decisions and wishful thinking.

That's for the "let's infer stuff" part. In a prediction or point estimation context, I can also try to explain how Bayesian procedures are well suited to hierarchical modelling and convenient computational algorithms, how they can be used to incorporate prior information, have nice properties and follow conceptually simple principles which are well suited to mathematical analysis. They may or may not help solving a particular problem and that's perfectly fine, but they are still a subject of study worthwhile of specialisation.

This post is about some of these nice properties of posterior distributions that I like to talk about. I'll leave the non-nice things for another time!

## 1. Point estimation and minimal expected risk

This first section is not directly about properties of the posterior distribution, but it rather concerned with some summaries of the posterior which have nice statistical properties in different contexts.

### Squared error loss

Suppose $\pi$ is a prior on an **euclidean** parameter space $\Theta \subset \mathbb{R}^d$ with norm $\|\theta\|^2 = \theta^T \theta$ defined through the dot product. Given a likelihood $p_\theta(X)$ for data $X$, the posterior distribution is defined as
$$
\pi(A \mid X) \propto \int_A p_\theta(X) \pi(d\theta)
$$
and the mean of the posterior distribution is
$$
\hat \theta_{\pi} = \int \theta \,\pi(d\theta \mid X) = \mathbb{E}_{\theta \sim \pi}[\theta \mid X].
$$
If we define the *risk* of an estimator $\hat \theta$ for the estimation of a parameter $\theta_0$ as
$$
R(\hat \theta; \theta_0) = \mathbb{E}_{X \sim p_\theta}[\|\theta_0 - \hat \theta(X)\|^2],
$$
and if 
$$
B_\pi(\hat \theta) = \mathbb{E}_{\theta_0 \sim \pi}[R(\hat \theta; \theta_0)]
$$
is the expected risk of $\hat \theta$ with respect to the prior $\pi$ (also called the **Bayes risk**), then we have that the posterior mean estimate $\hat \theta_{\pi}$ satisfies
$$
B_\pi(\hat \theta) \geq B_\pi(\hat \theta_\pi)
$$
for any estimator $\hat \theta$. That is, the posterior mean estimate minimizes the expected risk.

The proof follows from the fact that
$$
\| \theta_0 - \hat \theta(X) \|^2 \geq \|\theta_0 - \hat \theta_\pi(X) \|^2 + \langle \theta_0 - \hat \theta_\pi(X), \hat \theta_\pi(X) - \hat \theta(X)\rangle.
$$
Writing the expected risk as an expected posterior loss, i.e. using the fact that
$$
\mathbb{E}_{\theta_0 \sim \pi}\left[\mathbb{E}_{X \sim p_{\theta_0}}[\,\cdot\,]\right] = \mathbb{E}_{X \sim m}\left[\mathbb{E}_{\theta_0 \sim \pi(\cdot \mid X)}[\,\cdot\,]\right]
$$
where $m$ has density $m(x) = \int p_\theta(x) \pi(\theta)\,d\theta$, and since
$$
\mathbb{E}_{\theta_0 \sim \pi(\cdot \mid X)}\left[\langle \theta_0 - \hat \theta_\pi(X), \hat \theta_\pi(X) - \hat \theta(X)\rangle\right] = 0,
$$
we obtain the result.

A few remarks:

1. The expected risk has stability properties. If $\tilde \pi$ and $\pi$ are two priors that are absolutely continuous with respect to each other, and if $\|\log \frac{d\tilde \pi}{d\pi}\|_\infty \leq C$, then
   $$
   e^{-C}B_\pi(\hat\theta) \leq B_{\tilde \pi}(\hat \theta) \leq e^C B_{\pi}(\hat \theta).
   $$
   If the risk $R(\hat \theta; \theta_0)$ is uniformly bounded by some constant $M$ over $\theta_0\in \Theta$, then
   $$
   B_{\tilde \pi}(\hat \theta) \leq \sqrt{M B_{\pi}(\hat \theta)} \left\|d\tilde\pi/d\pi\right\|_{L^2(\pi)}.
   $$
   This shows how small chances in the prior does not result in a dramatic change in the expected loss of an estimator, as long as the priors have "compatible tails" (i.e. a manageable likelihood ratio).

2. It is sometimes advocated to choose the prior $\pi$ so that the risk $R(\hat \theta_\pi; \theta_0)$ is constant over $\theta_0$: the resulting estimator $\hat \theta_\pi$ is then agnostic, from a risk point of view, to $\theta_0$. This may result in a sample-size dependent prior (which is arguably not in the Bayesian spirit), but the fun thing is that it makes the expected risk *maximal* and the Bayes estimator $\hat \theta_\pi$ minimax: $\hat \theta_\pi \in \arg\min _ {\hat\theta} \sup _ {\theta_0}R(\hat \theta;\theta_0)$. Indeed, in that case we have for any estimator $\hat \theta$ that $\sup_{\theta_0} R(\hat \theta; \theta_0) \geq B_\pi(\hat \theta) \geq B_\pi(\theta_\pi) = \sup_{\theta_0}R(\hat \theta_\pi;\theta_0)$, from which it follows that $\hat \theta_\pi$ is minimax.

3. The idea of minimizing expected risk is not quite Bayesian, since it required us to first average over all data possibilities when computing the risk. One of the main advantage of the Bayesian framework is that it allows us to *condition* over the observed data, rather than pre-emptively considering all possibilities, and we can try to make use of that. Define the **posterior expected loss** (or **posterior risk**) or an estimator $\hat \theta$, conditionally on $X$, as
   $$
   R_\pi(\hat \theta\mid X) = \mathbb{E}_{\theta_0 \sim \pi(\cdot \mid X)}\left[(\hat \theta(X) - \theta_0)^2\right].
   $$
   It is clear from the previous computations that the posterior mean estimate minimizes the posterior risk, and hence the two approaches are equivalent. It turns out that, whatever the loss function we consider (under some regularity condition ensuring that stuff is finite and minimizers exist), minimizing the posterior risk is equivalent to minimizing the Bayes risk. In other words, we have that for any loss function $\ell \geq 0$ (again under some regularity conditions ensuring finiteness and existence of stuff), we have
   $$
   \arg\min_{\hat \theta}\mathbb{E}_{X \sim m}\left[\mathbb{E}_{\theta_0 \sim \pi(\cdot \mid X)}[\ell(\hat \theta(X), \theta_0)]\right] = \arg\min_{\hat\theta}\mathbb{E}_{\theta_0 \sim \pi(\cdot \mid X)}[\ell(\hat \theta(X), \theta_0)].
   $$
   This is roughly self-evident if we think about it.

## 2. Randomized estimation and minimal divergence



## 3. Online learning and minimal regret



## 4. Model selection, adaptability and oracle property





