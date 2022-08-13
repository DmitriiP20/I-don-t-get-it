---
layout: post
categories: [ANN, Gaussian Processes]
title: "Large Width Neural Networks and Gaussian Processes. Neural Tangent Kernel"
---

Around a month ago I set out to learn about the connection between Neural Networks (NN) and Gaussian Processes (GP), something that had been appearing more and more in the seminars I had been attending and literature I had been reading at the time.

This connection is _theoretically_ interesting because of the following. Standard NNs belong to the classical parametric frequentist approach to statistical learning. On the other hand, GP is a nonparametric modeling technique that belongs to the realm of Bayesian inference. On the _practical_ side, this connection sheds light on the training dynamics of a NN as I will explain below. Plus, GPs are classical objects that have been studied for much longer time compared to deep NNs.  

## Refresher on Gaussian Processes

Every parametric model with $n$ inputs and $m$ outputs defines a function $F_{W}: \mathbb{R}^n \to \mathbb{R}^m$ that depends on the chosen parameters $W$. In the Bayesian approach, one starts with a _prior_ distribution $p(W)$ over the _parameters_ $W$. This in turn induces a distribution over functions $\\{ F_W \\}\_W$ due to the above  identification $W \mapsto F_W$. This distribution lives directly in the function space. 

This observation tempted researchers to consider distributions directly in the function space $\mathcal{F}=\\{ F: \mathbb{R}^n \to \mathbb{R}^m \\}$. However, if trying to do this on the nose one quickly runs into all sorts of mathematical complications due to the fact that the function space $\mathcal{F}$ is too large even if one imposes regularity conditions on the functions such as continuity, smoothness, etc.

In the early XX century scientists found a way to circumvent this problem by coming up with a way of encoding the distribution over functions using finite/countable descriptions as follows. For simplicity we will consider functions with scalar output $f: \mathbb{R}^n \to \mathbb{R}$. A distribution over functions $\\{ f(x) \\}$  is a _Gaussian Process_ if conditional on any set of inputs $x_1, ..., x_n$ ( $n$ is arbitrary) the set of values $f(x_1), ..., f(x_n)$ is jointly normal  and the covariance matrix is given by $\Sigma_{i,j} = \mathcal{K}(x_i, x_j)$ for a fixed function $\mathcal{K}: \mathbb{R}^n \times \mathbb{R}^n \to \mathbb{R}$. Here one should think of the value $f(x)$ as being sampled from the distribution over functions for a fixed $x$. Furthermore,  $\mathcal{K}$ has to satisfy the appropriate symmetricity and positivity conditions so as to produce a valid covariance matrix.
More succinctly

$$ \forall n \quad \forall x=(x_1, ..., x_n): \\ (f(x_1), ... , f(x_n) ) | x \sim N(\mu(x), \Sigma(x)), \quad \Sigma(x)_{i,j} = \mathcal{K}(x_i, x_j).$$ 

To see that such a gadget indeed encodes a distribution over functions consider the following simple scenario. If you want to have a distribution where increasing functions are more probable than decreasing, then for $x_1 < x_2$ one just have to specify that the joint normal distribution of $f(x_1), f(x_2)$ is "concentrated" above the line $f(x_1) = f(x_2)$ (where, I remind you, $f(x_1)$ and $f(x_2)$ are random given $x_1$ and $x_2$).

## Untrained Wide Neural Nets are Gaussian Processes
