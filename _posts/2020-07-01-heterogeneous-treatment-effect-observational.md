---
title: "Heterogeneous treatment effect estimation with observational data"
date: 2020-07-01
categories:
  - blog
tags:
  - causal inference
  - causal ml
  - uplift modeling
  - heterogeneous treatment effects
---

When we released [Causal ML](https://github.com/uber/causalml), we didn't expect many people to be interested in using the package with observational data. Historically, uplift modeling algorithms have been used to gain additional insights from randomized experiments, so researchers in the area tended to take [ignorability](https://en.wikipedia.org/wiki/Ignorability) as a starting point.

However, based on the questions we've received since releasing Causal ML, it turns out there are now many people who are interested in using uplift modeling algorithms with observational data. For example, recently [a user asked](https://github.com/uber/causalml/issues/204) what we mean when we (admittedly very vaguely) state that "extra caution" is needed when applying uplift modeling algorithms to observational data, and what's missing from the library in terms of the ability to run observational analysis. I'm quoting my response below:

> Thanks for the great question. There's nothing missing from the package when it comes to observational data. It's just that the uplift modelling methods we've implemented assume what's often called [conditional ignorability](https://en.wikipedia.org/wiki/Ignorability), which is broadly speaking the idea that your feature set X contains the relevant confounders, or more specifically blocks any [back-door paths](http://bayes.cs.ucla.edu/BOOK-2K/ch3-3.pdf) between the candidate cause and the outcome of interest.

> In randomised experiments, the ignorability assumption is satisfied by design. In observational studies, we cannot tell for sure whether it is satisfied or not. Instead, we usually need to rely on subject matter expertise to determine what the relevant back-door paths could be, and what variables we need to "control for" to be able to estimate the treatment effect that we are interested in. When we talk about "extra caution" in the context of observational studies, we refer to the need for substantive subject matter expertise.

> There is another interesting problem when it comes to heterogeneous treatment effect estimation with observational data, which is that there is very little systematic research on how the different algorithms break down in the presence of confounders, both measured and unmeasured. Consequently, we are currently not able to recommend a particular algorithm for observational data, or tell you how badly your estimates are going to be wrong under different confounding scenarios. I'd expect some researchers to be working on this problem given that there seems to be a lot of demand for heterogeneous treatment effect estimation in observational studies.

It'll be interesting to see in the next few years whether we'll see more focus on observational data in the uplfit modeling literature. As mentioned above, I think the lack of research in this area is mostly a historical accident. It seems like uplift modeling is gaining popularity well beyond the initial use case of simple A/B tests.