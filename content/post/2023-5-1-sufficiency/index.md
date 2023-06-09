---
title: "Sufficiency"
author: "Ting Huang, Hongyi Liu, Alex McCreight"
bibliography: ref.bib
date: 2023-05-01
categories: ["R"]
tags: ["R Markdown", "plot", "regression"]
---

# Review of Properties of Estimators

## Preface

Sufficiency is an important property of an estimator in statistics, which indicates that an estimator contains all the relevant information about the population parameter being estimated. Unbiasedness, efficiency, and consistency are related to sufficiency in the sense that these properties help evaluate the quality of an estimator. A sufficient estimator that is unbiased, efficient, and consistent would be considered an ideal estimator, as it would provide accurate estimates, achieve the smallest possible variance, and improve in accuracy as the sample size increases, all while using the most relevant information available in the sample data.

## Unbiasedness

### Formal Definition

Suppose that `\(Y_1, Y_2, \dots , Y_n\)` is a random sample from the continuous pdf `\(f_Y(y; \theta)\)`, where `\(\theta\)` is an unknown parameter. An estimator `\(\hat{\theta} [=h(Y_1, Y_2, \dots, Y_n)]\)` is said to be unbiased (for `\(\theta\)`) if `\(E(\hat{\theta}) = \theta\)` for all `\(\theta\)`.

### Asymptotically Unbiased

An asymptotically unbiased estimator may be biased for small sample sizes, however, as the sample increases its bias will decrease. We can connect this to our original definition of an unbiased estimator by including a limit as the sample approaches infinity.

`\(\lim\limits_{n\rightarrow\infty}E(\hat{\theta}_n)-\theta=0\)`

## Efficiency

### Relative Efficiency

We can compare the efficiency of two unbiased estimators by finding which one has the lower variance. Let `\(\hat{\theta}_1\)` and `\(\hat{\theta}_2\)` be unbiased estimators of an unknown parameter `\(\theta\)`. If `\(Var(\hat{\theta}_1) < Var(\hat{\theta}_2)\)`, then we can say that `\(\hat{\theta}_1\)` is *more efficient* than `\(\hat{\theta}_2\)`.

### Cramer-Rao Lower Bound

**Theorem**: Let `\(Y_1, \dots Y_n\)`be a random sample from a continuous pdf `\(f_Y(y; \theta)\)`, and let `\(\hat{\theta} = g(Y_1, \dots, Y_n)\)` be any unbiased estimator for `\(\theta\)`. Suppose that `\(f_Y(y; \theta)\)` has continuous first- and second-order derivatives. Also, suppose that the set of y values where `\(f_Y(y; \theta) \neq 0\)` does not depend on `\(\theta\)`. Then, `\(Var(\hat{\theta}) \geq \frac{1}{I(\theta)}\)`, where `\(I(\theta)\)` is defined as `\(I(\theta) = E\Big[\Big(\frac{d}{d\theta}lnL(\theta)\Big)^2\Big]\)`.

Now, we can finally define an estimator to be efficient if it achieves the lowest possible variance among all unbiased estimators for a given parameter. In other words, the estimator’s variance will be equal to `\(\frac{1}{I(\theta)}\)`.

## Consistency

An estimator is considered efficient if it converges in probability to the true parameter value as the sample approaches infinity. More formally, we can say that an estimator `\(\hat{\theta}_n = h(W_1, W_2,\dots, W_n)\)` is said to be *consistent* for `\(\theta\)` if it converges in probability to `\(\theta\)`, that is, if for all `\(\epsilon > 0\)`, `\(\stackrel{lim}{n\rightarrow \infty}P(|\hat{\theta}_n-\theta|<\epsilon)=1\)`.

## Introduction to Sufficiency

A statistic is a function of some random sample of a population and we often use statistics as estimators for true population parameters since these parameters are almost always unknown. For any given random sample, there many functions of that random sample, so when we are looking for good estimators, should we be looking at each and every function of the random sample? No, instead we can look at a smaller subset of these functions of the random sample that give us the same amount of information as knowing the entire random sample. We call these statistics, sufficient statistics.
Let’s say we have a random sample of size `\(n\)`, `\(X_1, X_2, ..., X_n\)` from a probability distribution with an unknown parameter `\(\theta\)`, and we define a statistic `\(Y\)` as a function of this random sample:
`$$Y = u(X_1, X_2, ...,X_n)$$`
`\(Y\)` is said to be sufficient for `\(\theta\)` if the conditional distribution of `\(X_1, X_2, ..., X_n\)` given the statistic `\(Y\)`, does not depend on `\(\theta\)`. In other words, `\(Y\)` is a sufficient statistic if the person who knows the value of `\(Y\)` can do just as good of a job of estimating the unknown parameter `\(\theta\)` as someone who knows the entire random sample.
\## Example of Being Sufficient
This is an example of what it means for something to be sufficient. To be clear, this is not an example of a sufficient statistic.
Let’s say we roll a pair of fair dice without being allowed to view the outcome and we want to calculate the probability that the sum showing is an even number. Without any other information, the answer is `\(\frac{1}{2}\)` since the result is either even or odd. Now suppose that two other people were allowed to see the result, and let’s say the result was 7, and each is allowed to characterize the outcome without providing us the exact sum.
Person A tells us that the sum was less than or equal to 7 and person B tells us that the sum was odd. Whose information is more useful? Person B’s information is more useful and we can calculate the conditional probabilities to see why.
With person A’s information, the conditional probability would be
`$$P(\text{sum is even}|\text{sum} \leq 7) = \frac{P(\text{sum is even} \cap \text{sum} \leq 7)}{P(\text{sum} \leq 7)}$$`
`$$= \frac{P(2) + P(4) + P(6)}{P(2) + P(3) + P(4) + P(5) + P(6) + P(7)}$$`
`$$= \frac{\frac{1}{36}+\frac{3}{36}+\frac{5}{36}}{\frac{1}{36} + \frac{2}{36} + \frac{3}{36} + \frac{4}{36} + \frac{5}{36} + \frac{6}{36}} = \frac{9}{21}$$`
In contrast, Person B’s information gives us this conditional probability,
`$$P(\text{sum is even|sum is odd}) = 0$$`
Person B’s information clearly gives us more information and actually helps us answer the question of whether the dice roll is even or odd. In this sense, person B’s information is sufficient while person A’s is not.

## Example of a Sufficient Statistic

To give an example of how we can use the formal definition of sufficiency to find sufficient statistics, let’s use a Bernoulli pdf. Suppose that a random sample of size `\(n\)`, `\(X_1 = k_1, ..., X_n = k_n\)` is taken from a Bernoulli pdf,
`$$p_x (k;p) = p^k (1-p)^{1-k}, k = 0,1$$`
where `\(p\)` is an unknown parameter.
From our work with MLEs we know that our maximum likelihood estimator is
`\(\hat{p} = \frac{1}{n} \sum_{i = 1}^n X_i\)`
and that our maximum likelihood estimate is `\(p_e = \frac{1}{n} \sum_{i=1}^n k_i\)`.
We want to show that `\(\hat p\)` is a sufficient estimator for `\(p\)` so we need to calculate the conditional probability that `\(X_1 = k_1,...,X_n = k_n\)` given that `\(\hat p = p_e\)`.
`$$P(X_1 = k_1,...,X_n=k_n | \hat p = p_e) = \frac{P(X_1 = k_1,...,X_n = k_n \cap \hat p = p_e)}{P(\hat p = p_e)}$$`
`\(P(X_1 = k_1,...,X_n = k_n \cap \hat p = p_e) = 0\)` if `\(X_i \neq k_i\)` since this would mean that `\(\hat p \neq p_e\)`. Therefore
`$$P(X_1 = k_1,...,X_n=k_n | \hat p = p_e) = \frac{P(X_1 = k_1,...,X_n = k_n)}{P(\hat p = p_e)}$$`
But,
`\(P(X_1 = k_1,...,X_n = k_n) = p^{k_1}(1-p)^{1-k_1} * ...*p^{k_n}(1-p)^{1-k_n}\)`
\$ = p<sup>{*{i=1}^n k_i} (1-p)^{n-*{i=1}</sup>n} k_i\$.
We know that a Binomial distribution is the sum of individual independent Bernoulli’s so we can re-write this probability,
\$ = p<sup>{np_e}(1-p)</sup>{n-np_e}$. Now for the denominator, `\(P(\hat p = p_e) = P(\sum^n_{i=1}X_i = np_e) = ( {n \choose np_e} p^{np_e}(1-p)^{n-np_e})\)` because of the relationship between Binomials and Bernoulli's mentioned above. Therefore, `$$P(X_1 = k_1,...,X_n = k_n|\hat p = p_e) = \frac{p^{np_e}(1-p)^{n-np_e}}{{n \choose np_e} p^{np_e}(1-p)^{n-np_e}} = \frac{1}{{n \choose np_e}}$\$`Notice that this conditional probability is not a function of`(p)`indicating that`(p)`is a sufficient estimator for`(p)\`. Now in this instance, the conditional probability was easy to calculate but in most cases it will not be which is why we have the following Factorization Theorem to help us.

# Fischer’s Factorization Theorem

Given the definition of a sufficient statistic, we consider the immediate next-step question: how to propose, or prove, a sufficient statistic? Fisher’s Sufficiency Theorem is a fundamental result that helps to identify sufficient statistics for a given sampling from a model. In this Section, we will explain the theorem and its implications, and then demonstrate its application using Bernoulli samples as an example.

## The Factorization Theorem

Fisher’s Factorization Theorem states that a statistic `\(T(\boldsymbol{X})\)` is sufficient for a parameter `\(\theta\)` if and only if the joint probability distribution of the data `\(\boldsymbol{X}\)` can be factored into two components:

1.  A function `\(G(T(\boldsymbol{X}), \theta)\)` that depends on the data only through the sufficient statistic `\(T(\boldsymbol{X})\)`. This means that if two samples from the data of size `\(n\)` `\(\boldsymbol{X}=\{x_1,x_2,\cdots,x_n\}\)` and `\(\boldsymbol{Y}=\{y_1,y_2,\cdots,y_n\}\)`

2.  A function `\(H(\boldsymbol{X})\)` that does not depend on the parameter `\(\theta\)`.

Mathematically, the theorem can be expressed as:

$$
F(\boldsymbol{X} | \theta) = G(T(\boldsymbol{X}), \theta) H(\boldsymbol{X})
$$

where `\(F(\boldsymbol{X} | \theta)\)` is the joint probability distribution of the data `\(\boldsymbol{X}\)`, and `\(G\)` and `\(H\)` are the two factorized functions.

Note that if we are given a non-zero constant `\(c\)`, such that `$$G(T(\boldsymbol{X}) = G(cT^\prime(\boldsymbol{X})$$`, then `\(T^\prime(x)\)` is also a sufficient statistic. One constant that is often used is the size of the sample `\(n\)`, which we can assume to be known.

## Likelihood principle interpretation

An implication of the theorem is that when using likelihood-based inference, two sets of data yielding the same value for the sufficient statistic `\(T(X)\)` will always yield the same inferences about `\(\theta\)`. By the factorization criterion, the likelihood’s dependence on `\(\theta\)` is only in conjunction with `\(T(X)\)`. As this is the same in both cases, the dependence on `\(\theta\)` will be the same as well, leading to identical inferences.

Recall that the likelihood function is the joint probability of the observed data viewed as a function of the parameters. Thus, the factorization theorem can be applied to likelihood based methods. Incidentally, if we want to derive a Maximum Likelihood Estimator by taking the logarithm of the likelihood function and take its derivative, the part only containing `\(\boldsymbol{X}\)`, will vanish.

## Proving Sufficiency using Fischer’s Factorization Theorem

To prove that a statistic `\(T(\boldsymbol{X})\)` is sufficient for a parameter `\(\theta\)`, we need to show that the joint probability distribution `\(F(\boldsymbol{X} | \theta)\)` can be factored into the two components mentioned above. If this factorization is possible, then we can conclude that `\(T(\boldsymbol{X})\)` is sufficient for `\(\theta\)`.

## Example: Bernoulli Samples

Let’s consider a set of independent Bernoulli samples `\(\boldsymbol{X} = (X_1, X_2, ..., X_n)\)`, where each `\(X_i\)` has the probability mass function:

$$
f(x_i | p) = p^{x_i} (1 - p)^{1 - x_i}
$$

for `\(x_i \in \{0, 1\}\)` and `\(0 \le p \le 1\)`. Our goal is to prove that the sample sum `\(T(\boldsymbol{X}) = \sum_{i=1}^n X_i\)` is a sufficient statistic for the parameter `\(p\)`.

The joint probability mass function of the Bernoulli samples `\(\boldsymbol{X}\)` is given by:

$$
f(\boldsymbol{X} | p) = \prod_{i=1}^n p^{x_i} (1 - p)^{1 - x_i}
$$

Now, we can rewrite this expression as follows:

$$
f(\boldsymbol{X} | p) = p^{\sum_{i=1}^n x_i} (1 - p)^{n - \sum_{i=1}^n x_i}
$$

This can be further factored into:

$$
f(\boldsymbol{X} | p) = p^{T(\boldsymbol{X})} (1 - p)^{n - T(\boldsymbol{X})} \cdot 1
$$

In this case, we have:

$$
G(T(\boldsymbol{X}), p) = p^{T(\boldsymbol{X})} (1 - p)^{n - T(\boldsymbol{X})}
$$

and

$$
H(\boldsymbol{X}) = 1
$$

By applying Fisher’s Sufficiency Theorem, we can conclude that the sample sum `\(T(\boldsymbol{X}) = \sum_{i=1}^n X_i\)` is a sufficient statistic for the parameter `\(p\)`.

To further illustrate the usefulness of sufficiency, let’s consider estimating the parameter `\(p\)` using the Maximum Likelihood Estimation (MLE) method. The likelihood function for the Bernoulli samples is given by:

$$
L(p | \boldsymbol{X}) = \prod_{i=1}^n p^{x_i} (1 - p)^{1 - x_i}
$$

Taking the logarithm, we get the log-likelihood function:

$$
\log L(p | \boldsymbol{X}) = \sum_{i=1}^n x_i \log p + (1 - x_i) \log (1 - p)
$$

Taking the derivative with respect to `\(p\)` and setting it to zero, we obtain the MLE estimator for `\(p\)`:

$$
\hat{p} = \frac{T(\boldsymbol{X})}{n}
$$

This result shows that the MLE estimator of the parameter `\(p\)` depends only on the sufficient statistic `\(T(\boldsymbol{X})\)`, which further emphasizes the importance of sufficiency in statistical estimation.

To conclude, Fisher’s Sufficiency Theorem provides a powerful tool for identifying sufficient statistics in statistical models. By conditioning on sufficient statistics, we can extract all the relevant information needed for parameter estimation, thereby simplifying the estimation process and improving the quality of the estimators. The example with Bernoulli samples demonstrates the practical application of the theorem and highlights the benefits of using sufficient statistics in estimation tasks.

# The Rao-Blackwell Theorem

Now that we know how to define and prove a sufficient statistic, we conclude this project by a discussion of its utility. The Rao-Blackwell Theorem indicates that in terms of relative efficiency, a sufficient statistic always helps improve the quality of estimators. In this section, we will explain the theorem, its connection to sufficiency, and then demonstrate its application using Normal samples with a known mean and unknown variance as an example.

## Rao-Blackwell Theorem’s Statement

The Rao-Blackwell Theorem states that given an estimator `\(\hat{\theta}(\boldsymbol{X})\)` of a parameter `\(\theta\)` and a sufficient statistic `\(T(\boldsymbol{X})\)`, we can construct an improved estimator `\(\hat{\theta}^*(T(\boldsymbol{X}))\)` by conditioning on the sufficient statistic. The improved estimator has a smaller mean squared error (MSE) than the original estimator. Mathematically, the theorem is expressed as:

$$
\text{MSE}(\hat{\theta}^*(T(\boldsymbol{X}))) \le \text{MSE}(\hat{\theta}(\boldsymbol{X}))
$$

To compute the improved estimator, we calculate the conditional expectation:

$$
\hat{\theta}^*(T(\boldsymbol{X})) = \mathbb{E}[\hat{\theta}(\boldsymbol{X}) | T(\boldsymbol{X})]
$$

We will provide the following example to illustrate how Rao-Blackwell Theorem can improve the estimation, by attempting to estimate a sequence of Poisson distributed random variables (RVs) with unknown parameter `\(\lambda\)`. We will start with a “wild” estimator, `\(X_1\)`, which is the first random variable, and then apply the Rao-Blackwell Theorem to obtain an improved estimator.

In this example, we will apply the Rao-Blackwell Theorem to improve the estimation of the parameter of a sequence of Poisson distributed random variables (RVs) with an unknown parameter. We will start with a “wild” estimator, `\(X_1\)`, which is the value of the first RV, and then apply the Rao-Blackwell Theorem to obtain an improved estimator.

Let’s consider a set of independent Poisson distributed samples `\(\boldsymbol{X} = (X_1, X_2, ..., X_n)\)`, where each `\(X_i\)` has the probability mass function:

$$
P(X_i = k | \lambda) = \frac{e^{-\lambda} \lambda^k}{k!}
$$

with an unknown parameter `\(\lambda > 0\)`. Our goal is to estimate the parameter `\(\lambda\)`.

Let’s define the intentionally “wild” estimator as the value of the first RV:

$$
\hat{\lambda}_1 = X_1
$$

Notice that this estimator has a high variance, as it only considers the first RV and ignores the information from the remaining samples.

Then, we need to identify a sufficient statistic for the unknown parameter `\(\lambda\)`. According to the Factorization Theorem, the sum of Poisson distributed RVs is a sufficient statistic:

$$
T(\boldsymbol{X}) = \sum_{i=1}^n X_i
$$

Next, we need to compute the conditional expectation of the “wild” estimator given the sufficient statistic:

$$
\hat{\lambda}^{*}(\boldsymbol{X}) = \mathbb{E}[\hat{\lambda}_1 | T(\boldsymbol{X})]
$$

Note that `\(T(X)\)` is also Poisson Distributed,

$$
`\begin{align}
 & \sum_{i=1}^n \mathbb{E}[X_i\mid T(\boldsymbol{X}) = t] \\ &=   \mathbb{E}\left[\sum_{i=1}^nX_i\mid T(\boldsymbol{X}) = t \right] \\ &= \mathbb{E}\left[T(\boldsymbol{X})\mid T(\boldsymbol{X}) = t \right] \\&= t
\end{align}`
$$

Due to each `\(X_i\)` being independent and individually distributed,

$$
`\begin{align}
 & \hat{\lambda}^{*}(\boldsymbol{X}) = \mathbb{E}[\hat{\lambda}_1 | T(\boldsymbol{X})]\\ & = \frac{1}{n} \mathbb{E}\left[\sum_{i=1}^nX_i\mid T(\boldsymbol{X}) = t \right] \\ &= \frac{1}{n} \mathbb{E}\left[T(\boldsymbol{X})\mid T(\boldsymbol{X}) = t \right] \\&= \frac{t}{n} \\&= \frac{1}{n} \sum_{i=1}^n X_i \\ &= \bar{X}
\end{align}`
$$

This yields the Maximum Likelihood Estimator for `\(\lambda\)`, which is better in terms of relative sufficiency, as it meets the Cramer-Rao Lower Bound.

The Rao-Blackwell Theorem guarantees that the mean squared error (MSE) of the improved estimator `\(\hat{\lambda}^{*}(\boldsymbol{X})\)` is smaller than or equal to the MSE of the original “wild” estimator `\(\hat{\lambda}_1\)`.

# References:

(Casella and Berger 2021)
(Larsen and Marx 2013)

<div id="refs" class="references csl-bib-body hanging-indent">

<div id="ref-casella2021statistical" class="csl-entry">

Casella, George, and Roger L Berger. 2021. *Statistical Inference*. Cengage Learning.

</div>

<div id="ref-larsen2013introduction" class="csl-entry">

Larsen, Richard J, and Morris L Marx. 2013. *Introduction to Mathematical Statistics and Its Applications: Pearson New International Edition*. Pearson Higher Ed.

</div>

</div>
