---
layout: post
categories: [ANN], [Gaussian Processes]
title: "Large Width Neural Networks and Gaussian Processes. Neural Tangent Kernel"
---

Around a month ago I set out to learn about the connection between Neural Networks (NN) and Gaussian Processes (GP), something that had been appearing more and more in the seminars I had been attending and literature I had been reading at the time.

This connection is _theoretically_ interesting because of the following. Standard NNs belong to the classical parametric frequentist approach to statistical learning. On the other hand, GP is a nonparametric modeling technique that belongs to the realm of Bayesian inference. On the _practical_ side, this connection sheds light on the training dynamics of a NN as I will explain below. Plus, GPs are classical objects that have been studied for much longer time compared to deep NNs.  

## Refresher on Gaussian Processes

Every parametric model with $n$ inputs and $m$ outputs defines a function $F_{W}: \mathbb{R}^n \to \mathbb{R}^m$ that depends on the chosen parameters $W$. In the Bayesian approach, one starts with a _prior_ distribution $p(W)$ over the _parameters_ $W$. This in turn induces a distribution over functions $\\{ F_W \\}\_W$ due to the above  identification $W \mapsto F_W$. This distribution lives directly in the function space. 

### Stochastic Processes

This observation tempted researchers to consider distributions directly in the function space $\mathcal{F}=\\{ F: \mathbb{R}^n \to \mathbb{R}^m \\}$. However, one quickly runs into all sorts of mathematical complications due to the fact that the function space $\mathcal{F}$ is too large even if one imposes regularity conditions on the functions such as continuity, smoothness, etc.

In the early XX century scientists found a way to circumvent this problem by coming up with a way of encoding the distribution over functions using finite/countable descriptions. 
