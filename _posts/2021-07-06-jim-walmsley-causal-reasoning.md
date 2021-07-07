---
title: "Jim Walmsley and the art of causal reasoning"
date: 2021-07-06
categories:
  - causal inference
  - endurance training
  - running
tags:
  - causal inference
  - endurance training
  - running
  - ultra running
  - counterfactuals
  - transportability
  - confounding
---

Jim Walmsley is probably one of the best endurance athletes in the world. He is the three-time winner of the [Western States 100-mile race](https://www.wser.org) and has [a number of records to his name](https://en.wikipedia.org/wiki/Jim_Walmsley). One of the most striking things about Walmsley is that he is self-coached. In addition to being a gifted athlete, he presumably needs to be a pretty sophisticated thinker when it comes to endurance training.

I got some insights into his thinking by listening to a [podcast](http://www.dylanbowman.com/the-pyllars-podcast/2020/12/16/jim-walmsley-set-big-goals) that Walmsley recorded towards the end of last year with his fellow ultra runner Dylan Bowman. The discussion itself is wide-ranging and detailed, but here I want to focus on three quotes that show how Walmsley reasons causally about his training. The quotes illustrate three aspects of the [science of causal inference](http://bayes.cs.ucla.edu/WHY/): counterfactuals, confounding and transportability.

## Counterfactuals

One of the things that Walmsley is famous for is his high volume approach to training. In his preparation for the most recent Western States race, for example, he logged training weeks of up to 200K of running. Here is his assessment of how the high volume approach has worked for him:

> **Walmsley**: From the very beginning I was kind of hooked on big mileage. I think luckily I do pretty well with that and it’s worked out all right. I think that’s more of a random chance because different people have different successes with intensities and volume. And especially health wise, so I’ve been a little lucky… Or who knows, *maybe I’d do better with a different intensity*.

Probably the most common type of flawed reasoning in endurance training goes as follows: “I did [sweet spot] training for 8 weeks and it raised my [functional threshold power]. Therefore [sweet spot] training is the best way to raise [functional threshold power].” You can replace the terms in brackets with other training methods or metrics but the point remains. The above quote from Walmsley clearly illustrates why the reasoning is faulty. To determine the best training method, it’s not sufficient to ask whether your metrics improved under a particular regime; the relevant question is whether they improved more than they _would have improved_ under an alternative regime. This is an example of [counterfactual inference](https://www.inference.vc/causal-inference-3-counterfactuals/).

## Confounding

> **Bowman**: Have you started to feel the consequences of the training that you’ve put in over the last 4-5 years?
>
> **Walmsley**: Well, I mean part of it is *to distinguish the difference between training load and getting a couple of years older*. A little bit one and the same, maybe.

Does high volume training lead to injury? Do I get more improvements if I train by power rather than by perceived effort? Does more than 7 hours of sleep per night lead to better time trial performance? You could try to answer these and similar questions by simply comparing the relevant populations:

* Those who train a lot versus those who don’t
* Those who train by power versus those who don’t
* Those who sleep more than 7 hours per night versus those who don’t

And if you did this, you’d most likely get it terribly wrong. Why? Because these populations are different _to begin with_. For example, those who sleep less could have other stressors in their life. If you observe that those who get little sleep perform worse in time trials, how do you distinguish the effect of poor sleep from the other things that are going on in these individuals’ lives?

Walmsley’s quote highlights the same point. Yes, he has accumulated a lot of miles, but also he is getting older. How can we know the contribution of each of these factors? To answer questions like these, we need to rely on causal inference.

## Transportability

>**Bowman**: Have you ever felt an urge to get a coach? Or what gives you the confidence in your own approach?
>
>**Walmsley**: I would say it comes from the lack of belief that *many other people know how to do ultra running any better than any one of us*.

The point underlying this quote is subtle but important. The science of endurance training tends to consist of results obtained in very specific populations such as professional athletes or untrained individuals. The results from these small and often low-quality studies get extrapolated in media and online forums, often accompanied by claims to the effect that``Science shows that everyone should do X and Y’’.  However, the question whether the results of a study transport into populations beyond the one in which the study was conducted is not easy to answer and requires [special tools](https://www.pnas.org/content/113/27/7345).

Walmsley’s quote shows a healthy skepticism towards the idea that training principles developed in other contexts are also relevant in ultra running.

## What’s the big deal? 

You don’t have to be an endurance training genius to understand the above points. In fact, I bet most people would agree they are just common sense. Yet a lot of effort is [currently wasted](https://totte.cc/causal%20inference/no-amount-of-machine-learning/) in trying to develop "AI coaches" with the help of standard machine learning methods, which are fundamentally unable to address any of the three problems illustrated by Walmsley’s quotes. Human coaches will have nothing to worry about as long as the most important questions in endurance training aren’t recognized for what they are: causal questions.