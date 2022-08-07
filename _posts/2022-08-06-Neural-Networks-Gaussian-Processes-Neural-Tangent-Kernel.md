---
layout: post
description: First post.
categories: [ANN], [Gaussian Processes]
title: "Neural Networks and Gaussian Processes. Neural Tangent Kernel"
---
Around a month ago I set out to learn about the connection between Neural Networks (NN) and Gaussian Processes (GP), something that had been appearing more and more in the seminars I had been attending and literature I had been reading at the time.

This connection is _theoretically_ interesting because of the following. Standard NNs belong to the classical parametric frequentist approach to statistical learning. On the other hand, GP is a nonparametric modeling technique that belongs to the realm of Bayesian inference. On the _practical_ side, GPs are classical objects that have been understood much better than deep NNs plus this connection sheds light on the training dynamics of a NN as I will explain below.

## Refresher on Gaussian Processes

Every parametric model with $n$ inputs and $m$ outputs defines a mapping $F_{\theta}: \mathbb{R}^n \to \mathbb{R}^m$ 
