---
layout: post
title: Bounding Gibbs posterior probabilities
categories: [Research, Bayesian Theory]
---

# Bounding Gibbs posterior probabilities

Suppose we have data $X\sim Q$ for some unknown distribution $Q$, that we have a model $\Theta$ and a loss function $\ell_\theta(X)$ measuring a cost associated with fitting the data $X$ using a particular $\theta\in\Theta$. Our goal is to use the data to learn about parameters which minimize the risk $R(\theta) = \mathbb{E}[\ell_\theta(X)]$. Here are two standard examples.

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

## Gibbs posterior distribution

Let $\pi$ be a prior on $\Theta$. We define the associated Gibbs posterior as the random probability distribution
$$
\pi(A \mid X) = \int_A e^{-\ell_\theta(X)}\,\pi(d\theta) \Big /\int_\Theta e^{-\ell_\theta(X)}\,\pi(d\theta).
$$
The functions $x \mapsto e^{-\ell_\theta(x)}$ are called **pseudo-likelihoods**, as they may not be integrable or may not integrate to a constant which is uniform over $\theta \in \Theta$.

In the context of integrable pseudo-likelihoods, the above can be re-interpreted as a regular posterior distributions built from density functions $f _ \theta(x) \propto e^{-\ell _ \theta(x)}$ and with a prior $\tilde \pi$ satisfying
$$
\frac{d\tilde \pi}{d\pi}(\theta) \propto \int e^{-\ell_\theta(x)}\,dx =: c(\theta).
$$
However, the reason we **cannot apply standard asymptotic theory** to the analysis of Gibbs posterior is that the quantity $c(\theta)$ will typically be sample-size dependent. That is, if $X=X^n=(X_1, X_2, \dots, X_n)$ for i.i.d. random variables $X_i$ and if the loss $\ell_\theta$ separates as the sum
$$
\ell_\theta(X) = \sum_{i=1}^nl_{\theta}(X_i),
$$
then $c(\theta) = \left(\int e^{-l_\theta(x_1)} \, dx_1\right)^n$.

 **The prior is tilted proportionally to the sample size**, and here I will show how, under regularity and complexity constraints, this tilting is such that the posterior distribution will concentrate around the minimizer of the risk $R(\theta) = \mathbb{E}[\ell_\theta(X)]$ rather than the Kullback-Leibler minimizer from the regular model $\{f_\theta : \theta \in \Theta\}$. 

While the **general idea is well-known**, my contribution here is the introduction of the concept of **separation $\alpha$-entropy** which is a local measure of prior complexity that I propose as a fundamental tool to the study of (Gibbs) posterior concentration in finite and large samples. It draws inspiration from the Hausdorff $\alpha$-entropy of [Xing (2009)](https://www.researchgate.net/publication/222429392_Sufficient_conditions_for_Bayesian_consistency), from the concept of $\delta$-separation discussed in [Choi (2008)](https://projecteuclid.org/euclid.imsc/1209398468), from the prior summability conditions of Barron (1986) and [Walker (2004)](https://projecteuclid.org/euclid.aos/1098883780), as well as from the type of "off-centered" Rényi divergences used in [Kleijn and van der Vaart (2006)](https://projecteuclid.org/euclid.aos/1151418243) and [Bhattacharya et al. (2019)](https://arxiv.org/pdf/1611.01125.pdf) for the study of posterior concentration under misspecification.

This separation $\alpha$-entropy is bounded by metric entropies and by the Hausdorff $\alpha$-entropy in typical cases, while it is also suited to the study of posterior concentration under misspecification and generalizes the "covering numbers for testing under misspecification" of Kleijn and van der Vaart (2006). It allows us to obtain posterior concentration results in Hellinger or Rényi-type neighborhoods while bypassing testing techniques, and it is therefore also suited to study the posterior concentration of Gibbs posteriors. 

## Rényi-type divergences

Recall that $X \sim Q$ for some unknown distribution $Q$, define the excess risk as
$$
d_0(\theta, \theta_0) = \mathbb{E}[\ell_\theta(X) - \ell_{\theta_0}(X)]
$$
and for $\alpha \in (0,1]$ let 
$$
d_\alpha(\theta, \theta_0) = -\alpha^{-1}\log \mathbb{E}[e^{\alpha(\ell_{\theta_0}(X) - \ell_{\theta}(X))}]
$$
be a Rényi-type divergence between $\theta$ and $\theta_0$. It follows from Jensen's inequality that $d_\alpha$ is decreasing in $\alpha$ with also $d_\alpha \leq d_0$. I've written a bit about these divergences in the context of regular posterior distributions [on here](https://mathstatnotes.wordpress.com/2019/03/30/some-comparison-inequalities-for-off-centered-renyi-divergences/).

## The separation $\alpha$-entropy

Given a subset $A\subset \Theta$, we let $\langle A \rangle$ denote the convexification of the set of pseudo-likelihoods $e^{-A} := \{x \mapsto e^{-\ell_\theta(x)} : \theta \in A\}$. That is, $\langle A\rangle$ consists of all functions of the form $x \mapsto \int_A e^{-\ell_\theta(x)}\,\pi_A(d\theta)$ where $\pi_A$ is a prior on $A$.

**Definition 1** ($\delta$-separation).
We say that $A \subset \Theta$ is $\delta$-separated from $\theta_0 \in \Theta$ with respect to the divergence $d_\alpha$ if, for every $f \in \langle A \rangle$,*
$$
d_\alpha(f, \theta_0) := -\alpha^{-1}\log\mathbb{E}\left[\left(f(X)e^{\ell_{\theta_0}(X)}\right)^\alpha\right] \geq \delta.
$$
*In the case where the set $A$ is $1$-mixable, meaning that $e^{-A}$ is a convex space of functions, then the above condition is equivalent to that of $d_\alpha(\theta, \theta_0) \geq \delta$ for every $\theta \in A$.*

*A collection of sets $\{A_i\}$, $A_i \subset \Theta$, is said to be $\delta$-separated with respect to $d_\alpha$ if every $A_i$ is $\delta$-separated with respect to $d_\alpha$.*

**Definition 2** (separation $\alpha$-entropy).
Recall that we have fixed a prior $\pi$ on $\Theta$ and a learning target $\theta_0 \in \Theta$. The separation entropy of a set $A \subset \Theta$, with separation parameter $\delta > 0$ and exponent $\alpha \in (0,1]$, is defined as*
$$
\mathcal{S}_\alpha(A, \delta) = \inf\, \alpha^{-1}\log \sum_{i=1}^\infty \pi(A_i)^\alpha
$$
*where the infimum is taken over all coverings $\{A_i\}$ of $A$ which are $\delta$-separated from $\theta_0$ with respect to $d_\alpha$. When no such covering exists, then we let $\mathcal{S}_\alpha(A, \delta) = \infty$.*

## Bounding Gibbs posterior probabilities

We can obtain posterior concentration bounds using standard techniques. Theorem 1 below, for instance, is inspired by Theorem 3.2 of [Bhattacharya et al. (2019)](https://arxiv.org/pdf/1611.01125.pdf). Our only innovation is the use of the separation $\alpha$-entropy which allows us to obtain more general results that are applicable to regular posterior distributions as well as fractional and generalized posteriors.

**Theorem 1** (Posterior concentration bound).
*Let $A \subset \Theta$, $\delta > 0$, $t > 0$ and define*
$$
B(\delta) = \left\{\theta \in \Theta : \mathbb{E}\left[\ell_\theta(X) - \ell_{\theta_0}(X)\right] < \delta,\, \mathbb{E}\left[\left(\ell_\theta(X) - \ell_{\theta_0}(X)\right)^2\right] < \delta\right\}.
$$
*With $\kappa = (1+t)^2/ \alpha$, the upper bound* 
$$
\log \pi(A \mid X) \leq \mathcal{S}_\alpha(A, \kappa \delta) - \log \pi(B(\delta)) - \delta t / \alpha
$$
*holds with probability at least $1-2/(\delta t^2)$.*

**Remark.** In order for $\mathcal{S}_\alpha(A, \kappa\delta)$ to be finite, it is necessary that $A \subset \{\theta : d_\alpha(\theta, \theta_0) \geq \kappa \delta\}$.

*Proof.*
We can suppose there exists a covering $\{A_i\}$ of $A$ which is $\kappa\delta$-separated from $\theta_0$ with respect to $d_\alpha$, as otherwise $\mathcal{S}_\alpha(A, \kappa \delta) = \infty$ and the upper bound is trivial. Fix $\gamma > 1$ and let $\{A_i\}$ be furthermore such that $\sum _ {i=1}^n \pi(A_i)^\alpha < \gamma \, e^{\alpha\mathcal{S}_\alpha(A, \kappa \delta)} $. Now write
$$
\pi(A \mid X)^\alpha \leq \sum_{i=1}^\infty \pi(A_i\mid X)^\alpha = \frac{\sum_{i=1}^\infty \pi(A_i)^\alpha \left(\int_{A_i} e^{\ell_{\theta_0}(X)-\ell_\theta(X)}\,\pi_{A_i}(d\theta)\right)^\alpha}{\left( \int_{\Theta} e^{\ell_{\theta_0}(X) - \ell_{\theta}(X)} \,\pi(d\theta) \right)^\alpha}.
$$
We separately bound the numerator and denominator, following standard techniques. First, for any $t_1 > 0$, applying Markov's inequality yields
$$
\mathbb{P}\left(\sum_{i=1}^\infty \pi(A_i)^\alpha \left(\int_{A_i} e^{\ell_{\theta_0}(X)-\ell_\theta(X)}\,\pi_{A_i}(d\theta)\right)^\alpha >  \gamma e^{\alpha\mathcal{S}_\alpha(A, \kappa\delta) - t_1\delta}\right) 
\\ \leq \frac{e^{\alpha t_1\delta} \sum_{i=1}^\infty\pi(A_i)^\alpha \mathbb{E}\left[\left(e^{\ell_{\theta_0}(X)} \int_{A_i}e^{-\ell_\theta(X)} \pi_{A_i}(d\theta)\right)^\alpha\right]}{\gamma e^{\alpha\mathcal{S}_\alpha(A, \kappa \delta)}}
\leq e^{-\delta (\alpha\kappa-t_1)} 
$$
For the denominator, we have, for any $t_2 > 1$, that
$$
\mathbb{P}\left( \left( \int_{\Theta} e^{\ell_{\theta_0}(X) - \ell_{\theta}(X)} \,\pi(d\theta) \right)^\alpha < \pi(B(\delta))^\alpha e^{-t_2\alpha\delta}\right) \leq \frac{1}{\delta(t_2-1)^2}.
$$
This follows along the lines of Lemma … of … . Combining the above yields that
$$
\log \pi(A\mid X) \leq \alpha^{-1}\log\gamma + \mathcal{S}_\alpha(A, \kappa \delta) - \log \pi(B(\delta)) - \delta(\alpha^{-1}t_1 - t_2)
$$
holds with probability at least $1-e^{-\delta(\alpha\kappa-t_1)}-\frac{1}{\delta(t_2-1)^2}$. In particular, taking $t_2 = t+1$, $t_1 = 2t+1$ and $\kappa = (t+1)^2/\alpha$, we obtain from $\alpha^{-1}t_1 - t_2 = \alpha^{-1}(2t+1)-t-1 \leq t/\alpha$ that 
$$
\log \pi(A\mid X) \leq \alpha^{-1}\log\gamma + \mathcal{S}_\alpha(A, \kappa \delta) - \log \pi(B(\delta)) - \delta t/\alpha
$$
holds with probability at least 
$$
1-e^{-\delta(\alpha\kappa-t_1)}-\frac{1}{\delta(t_2-1)^2} = 1-e^{-\delta t^2} - 1/(\delta t^2) \geq 1-\frac{2}{\delta t^2}.
$$
Letting $\gamma \rightarrow 1$ then yields the general result. $\Box$

The constants $t_1, t_2$ and $\kappa$ used in the proof could be better chosen to give more freedom in tuning the theorem. See e.g. what's done in Bhattachary et al. (2019).

## Large samples

Suppose now that $\Theta$ parameterizes a sequence $\ell^{(n)}_\theta$ of loss functions corresponding to a sequence of  independent and identically distributed observations $X^{(n)} = (X_1, X_2, \dots, X_n)$, with $X_i \sim Q$, and that the loss $\ell^{(n)}_\theta$ splits as a sum as
$$
\ell^{(n)}_\theta(X^{(n)}) = \sum_{i=1}^n \ell_\theta(X_i)
$$
In that context, with
$$
\pi(A \mid X^{(n)}) \propto \int_A e^{-\sum_{i=1}^n\ell_\theta(X_i)}\,\pi(d\theta),
$$
Theorem 1 can be reinterpreted as follows.

**Corollary 1** (Posterior concentration bound, i.i.d. case).
*Let $A \subset \Theta$, $\delta > 0$, $t > 0$ and define*
$$
B(\delta) = \left\{\theta \in \Theta : \mathbb{E}\left[\ell_\theta(X) - \ell_{\theta_0}(X)\right] < \delta,\, \mathbb{E}\left[\left(\ell_\theta(X) - \ell_{\theta_0}(X)\right)^2\right] < \delta\right\}.
$$
*With $\kappa = (1+t)^2/ \alpha$, the upper bound* 
$$
\log \pi(A \mid X^{(n)}) \leq \mathcal{S}_\alpha(A, \kappa \delta) - \log \pi(B(\delta)) - n \delta t / \alpha
$$
*holds with probability at least $1-2/(n\delta t^2)$.*

### Asymptotics

**Theorem 2** (Posterior consistency).
*Recall that $d_0(\theta, \theta_0) = \mathbb{E}[\ell _ {\theta}(X) - \ell _ {\theta_0}(X)]$ is the excess risk and suppose there exists a $\delta > 0$ such that*
$$
\pi\left( \left\{ \theta \in \Theta: d_0(\theta, \theta_0) < \delta \right\} \right) > 0.
$$
*If $A \subset \Theta$ is such that $\mathcal{S}_\alpha(A, \delta) < \infty$ for some $\alpha \in (0,1]$, then*
$$
\pi(A \mid X^{(n)}) \rightarrow 0
$$
*almost surely as $n \rightarrow \infty$.*

## Upper bounding the separation $\alpha$-entropy

Always, for $A = \{\theta : d_1(\theta, \theta_0) > \delta\}$, we have $\mathcal{S}_1(A, \delta) = \log \pi(A)$.

More generally, I wrote a bit about the problem of bounding the separation $\alpha$-entropy [on here](https://mathstatnotes.wordpress.com/2019/04/08/posterior-concentration-in-terms-of-the-separation-alpha-entropy/). 

Basically the idea is to upper bound the separation $\alpha$-entropy through the metric entropy of $d_\alpha$-spheres around $\theta_0$. If the spheres around $\theta_0$ have infinite metric entropy, then we can split the model as $\Theta = \bigcup_{i=1}^\infty \Theta_i$ and upperbound $\mathcal{S}_\alpha$ by $\sum_{i=1}^\infty \pi(\Theta_i) N_i$, where $N_i$ is the metric entropy of the spheres around $\theta_0$ intersected with $\Theta_i$. The idea is from Xing (2009) and I did something similar in my paper [Bayesian Nonparametrics for Directional Statistics](https://arxiv.org/abs/1807.00305) in order to bound the Hausdorff $\alpha$-entropy of my model. This allows us to get somewhat explicit bounds on the Hausdorff $\alpha$-entropy which also upper bounds the separation $\alpha$-entropy in the well-specified case.

## Conceptual applications

### Fractional posterior distributions

Consider for simplicity the well-specified case where $X_i \sim^{i.i.d.} p_{\theta_0}$ for some density $p_{\theta_0}$ corresponding to $\theta_0 \in \Theta$. The loss corresponding to fractional posterior distributions with parameter $\eta \in (0,1)$ is
$$
\ell_\theta(X) = (p_\theta(X))^\eta,
$$
$d_0(\theta, \theta_0)$ is the Kullback-Leibler divergence between $p_\theta$ and $p _ {\theta_0}$ and
$$
d_1(\theta, \theta_0) = -\eta \log\mathbb{E}\left[\left(p_\theta(X)/p_{\theta_0}(X)\right)^\eta\right]
$$
is topologically equivalent to the Hellinger distance $H$ (more precisely, $d_1$ is comparable to $-2\log(1-H(\theta, \theta_0)^2)$. Therefore, Theorem 2 above immediately implies the Hellinger consistency of Bayesian fractional posteriors over its Kullback-Leibler support, with the entropy condition $\mathcal{S}_\alpha(A, \delta) < \infty$ being automatically satisfied when taking $\alpha = 1$.

### Regular posterior distributions

Taking $\eta = 1$ above yields regular posterior distributions. In this case, Theorem 2 above implies as a corollary basically any Hellinger posterior consistency that appeared in the literature (here our result is stated in slightly weaker form than it could be, but in its strong form it implies every previous result that appeared in the literature of Hellinger posterior consistency.) This is because, in the well-specified regular case, the separation $\alpha$-entropy is upper bounded by (function of) the widely used metric entropies and hausdorff $\alpha$-entropy.

In the misspecified case, I strongly suspect this separation $\alpha$-entropy is also upper bounded by the "covering numbers for testing under misspecification" of Kleijn and van der Vaart (2006), and therefore also generalizes their result (up to some technicalities that can happen in the tail of the models; this get a bit technical and I haven't yet precisely compared the two approaches.)

### Other things to explore:

- Upper bounding the separation $\alpha$-entropy can get messy. Can we ensure that $\mathcal{S}_1(A, \delta) = \log \pi(A)$ as is the case with fractional posterior distributions in more general situations? The problem amounts to ensuring that the divergence $d_1$ is interesting and that the neighborhood $A = \{\theta :d_1(\theta, \theta_0) > \delta \}$ is not empty. 

  In other words: whenever the function $d_1(\theta, \theta_0) = - \log \mathbb{E}[e^{\ell _{\theta _0}(X) - \ell _ \theta(X)}]$ is an interesting measure of divergence, then we can get correspondingly **interesting results without having to bother about the separation $\alpha$-entropy** (which we can explicitely compute in that case).


