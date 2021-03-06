---
layout: post
title: Maximum Likelihood Estimation
---
Maximum likelihood estimation method is frequently used in Standford CS229 notes for estimating the parameter of the machine learning models. This serves as simple guide and reference for understanding the key concepts.

[TOC]

## Likelihood Function

A ***likelihood function*** (often simply the likelihood) is a function of the parameters of a statistical model, given specific observed data.

It is important to distinguish between probability and likelihood. Probability describes the plausibility of a random outcome, given a model parameter value, without reference to any observed data. Likelihood describes the plausibility of a model parameter value, given specific observed data.

So it is possible that a parameter value or a statistical model have a large likelihood value for a given specified observed data, and yet have a low probability, or vice versa.

However, please note that the value of the likelihood function is *not* the probability of the specific parameter value, given the specific observed data.

### Discrete Probability Distribution

Let $X$ be a discrete random variable with probability mass function $p$ depending on a parameter $\theta$.

The likelihood function (of $\theta$, given the outcome $x$ of $X$), denoted $\mathcal{L}(\theta \mid x)$, is
$$
\mathcal{L}(\theta \mid x) = p_{\theta}(x) = P_{\theta}(X=x) = P(X=x \mid \theta)
$$
Often the last probability notation is written as $P(X=x; \theta)$ to emphasize it is not a conditional probability.

### Continuous Probability Distribution

Let $X$ be a continuous random variable with probability density function $f$ depending on a parameter $\theta$.

The likelihood function (of $\theta$, given the outcome $x$ of $X$), denoted $\mathcal{L}(\theta \mid x)$, is
$$
\mathcal{L}(\theta \mid x) = f_{\theta}(x)
$$

### Joint Probability Distribution

In many cases, we will look at a sample rather than a single observation.

Let $X$ be a discrete random variable with probability mass function $p$ depending on a parameter $\theta$, and $x_1, x_2, \dots, x_n$ be independent observations and identically distributed. The likelihood function is
$$
\begin{align}
\mathcal{L}(\theta \mid x_1, x_2, \dots, x_n) &= p(x_1, x_2, \dots, x_n) \\
&= p(X_1=x_1 \text{ and } X_2=x_2 \text{ and } \cdots \text{ and } X_n=x_n) \\
&= P(X_1=x_1)P(X_2=x_2) \cdots P(X_n=x_n) \\
&= \prod_{i=1}^n P(X=x_i)
\end{align}
$$
Similarly, in the continuous case, let $X$ be a continuous random variable with probability density function $f$ depending on a parameter $\theta$, and $x_1, x_2, \dots, x_n$ be independent observations. The likelihood function is
$$
\begin{align}
\mathcal{L}(\theta \mid x_1, x_2, \dots, x_n) &= f(x_1, x_2, \dots, x_n) \\
&= f(x_1)f(x_2) \cdots f(x_n) \\
&= \prod_{i=1}^n f(x_i)
\end{align}
$$

### Log-likelihood

Very often, the natural logarithm of the likelihood function, called the ***log-likelihood***, is more convenient to work with.

Usually we are interested in where the likelihood reaches its maximum. Since the natural logarithm is monotonically increasing, the point at which the log-likelihood reaches maximum is the same as where the original likelihood function reaches maximum.

In the case of the joint likelihood, the product terms become sum.
$$
\begin{align}
\ln \mathcal{L}(\theta \mid x_1, x_2, \dots, x_n) &= \ln \prod_{i=1}^n f(x_i) \\
&= \ln f(x_1)+\ln f(x_2)+ \cdots +\ln f(x_n) \\
&= \sum_{i=1}^n \ln f(x_i)
\end{align}
$$
Sum is a lot more easier to optimize than product, as the derivatives of sum is just the sum of the derivatives and we can also take advantage of many nice properties of logarithm.

## Maximum Likelihood Estimation

***Maximum likelihood estimation (MLE)*** is a method of estimating the parameters of a statistical model, given observations. MLE attempts to find the parameter values that maximize the likelihood function, given the observations.

Mathematically, to find maximum likelihood estimate $\hat{\theta}$,
$$
\hat{\theta} \in \{ \underset{\theta \in \Theta}{\operatorname{arg max}} \mathcal{L}(\theta;x) \} \quad \text{(if a maximum exists)}
$$
As mentioned above, in practice, it is often more convenient to work with the log-likelihood
$$
\ell(\theta;x)=\ln \mathcal{L}(\theta;x)
$$
or the average log-likelihood
$$
\hat{\ell}(\theta;x)=\frac{1}{n} \ln \mathcal{L}(\theta;x)
$$

### Find MLE

Using calculus knowledge, to find the maxima of the log-likelihood function (if it exists), we can

* Take first derivative of $\mathcal{L}(\theta;x)$ w.r.t $\theta$, and set it to 0.
* Take second derivative of $\mathcal{L}(\theta;x)$ w.r.t $\theta$, and confirm it is negative.

Note that this might not always lead to the global maximum (could be local maximum).
