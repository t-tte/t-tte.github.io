---
title: "Software and references for the talk on estimating individual treatment effects at KDD 2022"
date: 2022-08-14
categories:
  - causal inference
tags:
  - causal inference
  - software
  - causalml
---

Below are some references for the talk I'm giving at KDD in the [1st Workshop on End-End Customer Journey Optimization](https://sites.google.com/view/user-journey-kdd/home). I will update this post with additional materials as they become available. For the slides feel free to message me on any social media channels shown on the left hand side (if you message me on Strava, I will also send you bonus slides that didn't make it to the presentation).

## Papers

* [Tian and Pearl (2000): Probabilities of Causation](https://arxiv.org/pdf/1301.3898.pdf)
* [Li and Pearl (2019): Unit Selection Based on Counterfactual Logic](https://www.ijcai.org/Proceedings/2019/0248.pdf)
* [Mueller, Li, and Pearl "Causes of effects: Learning individual responses from population data](https://arxiv.org/pdf/2104.13730.pdf)
* [Mueller and Pearl "Personalized Decision Making -- A Conceptual Introduction](https://ftp.cs.ucla.edu/pub/stat_ser/r513.pdf)

## Software

* [CausalML PNS bounds](https://github.com/uber/causalml/blob/master/causalml/optimize/pns.py): Allows the user to calculate the probability of benefit (probability of necessity and sufficiency).
* [CausalML unit selection](https://github.com/uber/causalml/blob/master/causalml/optimize/unit_selection.py): Enables the user to assign weights to different responder types.
