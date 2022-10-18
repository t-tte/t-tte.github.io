---
title: "Heterogeneous treatment effect estimation with observational data, pt. II"
date: 2022-10-17
categories:
  - causal inference
tags:
  - causal inference
  - causal ml
  - uplift modeling
  - heterogeneous treatment effects
---

Two years ago I wrote a [post](https://totte.cc/causal%20inference/heterogeneous-treatment-effect-observational/) on using [Causal ML](https://github.com/uber/causalml) with observational data. I mentioned that, in developing Causal ML, we mostly had in mind the typical use case for [uplift modelling](https://en.wikipedia.org/wiki/Uplift_modelling), which is that of finding heterogeneous treatment effects in randomised experiments. To this date, I’ve never used Causal ML with observational data.

At Uber, where Causal ML was originally developed, we also worked on an internal Python package for observational causal inference. This piece of software was never open sourced, although some of its methods made their way into Causal ML as a kind of compromise. We noticed that some users wanted to adopt the package for observational causal inference and incorporated basic methods like propensity score matching and two-stage least squares. The reason why we didn’t include all of the observational causal inference capabilities developed internally at Uber is that we conceived of Causal ML as a package that is focused on uplift modelling.

Last week the author and developer Robert R Tucci published a [blog post](https://qbnets.wordpress.com/2022/10/12/incorrect-causal-inference-being-used-by-ubers-causalml-software-and-uplift-marketers-using-tree-methods-to-calculate-ate/) stating that Causal ML makes a “fundamental and glaring error” by promoting the use of machine learning to analyse observational data. In particular, he suggests that the developers of Causal ML promote a “kitchen sink” approach to causal inference, where you control for as many covariates as you can when estimating treatment effects in observational studies. He points out that the correct approach would be that of using a graphical causal model to select the relevant covariates.

Despite the dramatic tone of the blog post, there is no real disagreement here. Causal ML was built for analysing randomised controlled experiments and is successfully used for this purpose by individual users as well as some of the world’s biggest companies. The reason our documentation is not focused on the problems of observational causal inference is not because we erroneously believe that ML will somehow automatically take care of those problems. Rather, it’s because we intentionally focused on a data generating process that requires fewer assumptions. As regards the observational case, nothing has changed since I published the blog post two years ago: subject matter expertise is still required.
