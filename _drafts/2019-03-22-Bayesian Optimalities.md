---
layout: post
title: Bayesian Optimalities
categories: [Bayesian Theory]
---

# Bayesian Optimalities

I'm sometimes asked in conferences and meetings around Montreal: *why Bayes?* 

This always strikes me. I do sometimes identify with "bayesianism", because I want to do research related to Bayesian statistics, but I don't feel that I'm a Bayesian in the sense that I adhere to one particular school of thought. First and foremost, I am a mathematician and a statistician. I want to understand the world through simulation and modelling, with the certainty provided by mathematical lenses, and I want to understand and develop the statistical tools that we use to understand the world when certainty is not at reach. That's my scientific identity.

Yet I'm also driven to answer: *what else?* What else than probabilities to model uncertainty and randomness? What else than probabilistic conditioning to account for new information? (Ok, I'm exaggerating a bit here. There are tons of other fun "else" to answer that question, but Bayes certainly stands out.) I'm drawn to Bayesian stats because, more often than not, it's about providing meaningful answers to the questions that we really care about. I want, when possible, posterior probabilities of hypotheses; not 0-1 decisions and wishful thinking.

That's for the "let's infer stuff" part. In a prediction or point estimation context, I can also try to explain how Bayesian procedures are well suited to hierarchical modelling and convenient computational algorithms, can be used to incorporate prior information, have nice properties and follow conceptually simple principles which are well suited to mathematical analysis. They may or may not help solving a particular problem and that's perfectly fine, but they are still a subject of study worthwhile of specialisation.

This post is about some of these nice properties of posterior distributions that I like to talk about. I'll leave the non-nice things for another time!

## 1. Point estimation and minimal expected risk

This first section is not directly about properties of the posterior distribution, but it rather concerned with some summaries of the posterior which have nice statistical properties in different contexts.

### Squared error risk

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
is the expected risk of $\hat \theta$ with respect to the prior $\pi$, then we have that the posterior mean estimate $\hat \theta_{\pi}$ satisfies
$$
B_\pi(\hat \theta) \geq B_\pi(\hat \theta_\pi)
$$
for any estimator $\hat \theta$. That is, the posterior mean estimate minimises the expected risk.

A few remarks before the (simple) proof:

1. The expected risk has stability properties. If $\tilde \pi$ and $\pi$ are two priors that are absolutely continuous with respect to each other, and if $\|\log \frac{d\tilde \pi}{d\pi}\|_\infty \leq C$, then
   $$
   e^{-C}B_\pi(\theta_\pi) \leq B_{\tilde \pi}(\hat \theta_\pi) \leq e^C B_{\pi}(\hat \theta_\pi).
   $$
   If the risk $R(\hat \theta_\pi; \theta_0)$ is uniformly bounded by some constant $M$ over $\theta_0\in \Theta$, then
   $$
   B_{\tilde \pi}(\hat \theta_\pi) \leq \sqrt{M B_{\pi}(\hat \theta_\pi)} \left\|d\tilde\pi/d\pi\right\|_{L^2(\pi)}.
   $$
   

## 2. Randomised estimation and minimal divergence



## 3. Online learning and minimal regret



## 4. Model selection, adaptability and oracle property







