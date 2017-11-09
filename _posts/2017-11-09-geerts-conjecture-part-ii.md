---
layout: post
title: "Sum of Poisson and Gaussian Random Variables"
excerpt: "Dr. G's Conjecture part II"
modified: 2017-09-08
tags: [gsoc, astropy, openastronomy]
comments: true
image:
  feature: gsoc_post.jpg
  credit: Hubble Space Telescope
---

In the last blog post we did a basic derivation of the Poisson likelihood.

In this blog post I am going to derive the likelihood function of the sum between Poisson and Gaussian random variables.

This model appears in many practical scenarios, specially in imaging in which a photon noise component (usually Poisson distributed)
gets combined with a thermal noise component (usually assumed to be Gaussian distributed).

Consider an experiment that outputs $$Z_i = Y_i + X_i,~i=1, 2, ..., n$$. Assume that $$Y^{n}
\triangleq \{Y_i\}_{i=1}^{n}$$ is a sequence of independent but **not** identically distributed Poisson random variables,
each of which has mean $$\lambda_i(\theta)$$, where $$\theta$$ is a vector of parameters which belongs to some set
$$\Theta \subseteq \mathbb{R}^m$$ called parameter space. Assumed further that $$X^{n}
\triangleq \{X_i\}_{i=1}^{n}$$ is a sequence of iid Gaussian random variables with zero mean and variance $$\sigma^2$$, $$\sigma^2 > 0$$.

The first step into deriving the likelihood function of $$Z^{n}$$ is to get the pdf of every $$Z_i$$. Since $$Z_i$$ is the sum
of a Poisson random variable and a Gaussian random variable, we can go ahead and perform the convolution between their pdfs in
order to get the pdf of $$Z_i$$. However, let's try a different approach.

Note that, conditonal on $$ Y_i = yi$$, $$Z_i$$ follows a Gaussian distribution with mean $$\lambda_i(\theta)$$ and variance
$$ \lambda_i(\theta) + \sigma^2 $$, i.e.

$$
\begin{align}
p(z_i | y_i) = \dfrac{1}{\sqrt{2\pi(\lambda_i(\theta) + \sigma^2)}}\exp\left{-\dfrac{1}{2}\left(\dfrac{z_i - \lambda_i(\theta)}{\lambda_i(\theta) + \sigma^2}\right)^2\right}
\end{align}
$$

Now, we can use the Law of Total Probability to derive $$p(z_i)$$ as follows

$$
\begin{align}
p(z_i) = \mathbb{E}(p(z_i | Y_i)) = \sum_{i=0}^{\infty}p(z_i | y_i)p(y_i) = \sum_{i=0}^{\infty} \dfrac{1}{\sqrt{2\pi(\lambda_i(\theta) + \sigma^2)}}\exp\left{-\dfrac{1}{2}\left(\dfrac{z_i - \lambda_i(\theta)}{\lambda_i(\theta) + \sigma^2}\right)^2\right} \lambda_i(\theta)^{y_i}\dfrac{e^{-\lambda_i(\theta)}}{y_i!}
\end{align}
$$