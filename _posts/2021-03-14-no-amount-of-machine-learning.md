# No Amount of Machine Learning Will Tell You Why a Training Plan Works

## The Emergence of Big Data in Endurance Training
Endurance training is ripe for disruption. In recent years, there's been a sharp increase in the amount of data that amateur athletes can capture. For example, if you are a cyclist who uses some kind of structured training plan, you typically capture some data of your daily activities, including sleep, movement and in some cases nutrition. You may also record various types of body measurements, heart rate data, body temperature, and so on. When you do workouts, you additionally capture power, cadence, pedaling dynamics... the list goes on.

Of course, professional athletes have captured all of the above and more for years. What's new is the ability of amateur athletes to do the same. This means that there's now an unprecedented amount of data on endurance training. Yet the methods for endurance training have remained the same. If you are not working with an individual coach but still want to follow a structured training plan, your options are limited to stock programs that are all variations of a handful of basic approaches. Moreover, each individual training plan is the same for all of the athletes that are doing it. Usually, the only adjustment is based on a rough approximation of your [functional threshold power](https://www.trainingpeaks.com/learn/articles/what-is-threshold-power/).

## TrainerRoad's Adaptive Training 

Needless to say, the "one size fits all" approach discussed above is unlikely to produce optimal results. No wonder, then, that companies such as [TrainerRoad](https://www.trainerroad.com/adaptive-training/) are looking to change things. They are currently rolling out what they call "adaptive training", which leverages users' training history and other individual information to adjust their workouts. For example, if you fail to complete a given workout, the system may change the intensity of your following workout downwards. As simple as this sounds, it's already an improvement compared to standard stock plans where the next workout will remain the same irrespective of whether you can complete today's intervals or not.

From the [lengthy podcast](https://www.youtube.com/watch?v=nAYVLch8tEA&list=PLrKJ0zeMQrI61wqXR8MUBXBHPk5Rli1yH&index=3) in which TrainerRoad announced their plans to roll out adaptive training (also discussed [here](https://www.dcrainmaker.com/2021/02/trainerroad-adaptive-training-trainnow.html)), it's clear they view this as an initial step towards truly AI-based training. The eventual goal is to tailor entire training plans based on users' individual characteristics. Here, I started wondering whether the machine learning methods discussed in the podcast are up for the task. Without going too much into the details, the modeling approaches discussed in the podcast focus on the standard goals of machine learning: classification and prediction. For example, one of the ways in which adaptive training uses historical training data is to predict how likely you are to fail the next workout. Presumably, if the probability is too high, you will be prescribed another set of intervals.

If predicting the probability of failing a workout was the only thing we cared about, then standard machine learning would be the right tool for the task. However, to be able to devise truly individualized training plans, it is not sufficient to know _that_ someone's probability of failing the next workout is 0.3. What we really want to understand is _why_ that probability is 0.3. Moreover, to find the _optimal_ workout, we need to evaluate what that individual's performance _would_ be under different alternatives. For example, to know whether 4x5min intervals are optimal for me today, the AI needs to evaluate what my performance would look like if I did 6x3min intervals instead. In fact, it needs conduct this analysis for each possible interval structure. Standard machine learning methods cannot answer these types of questions, although it may initially look like as if they could.

## Machine Learning Doesn't Answer Why-Questions

If you want to use X to predict Y, it doesn't much matter whether X is a cause of Y or whether the two are merely correlated. The only thing you're interested in is whether X carries some information about Y, not _why_ it carries that information. Because machine learning methods are designed for the purposes of prediction, you cannot use them to "discover" the causes of Y, no matter how hard you try.

Here is a common way in which data scientists try to use machine learning models to "discover" the causes of Y: add new features into the model one by one and check if adding a given feature improves the accuracy of the model. If the answer is "yes", then that feature is a cause of Y; if the answer is "no", then that feature isn't a cause of Y.

The above is a fallacy because:
* X can be a cause of Y without improving the accuracy of a model used to predict Y
* X can improve the accuracy of a model used to predict Y without being a cause of Y

Let us illustrate both of these points. Consider first the following hypothetical structure:

```
Age -> Compliance Rate -> Failure
```

Let's imagine that older athletes are less likely to actually do the assigned workouts (Compliance Rate) and consequently more likely to fail the next workout (Failure). Now suppose that your machine learning model already includes Compliance Rate as a predictor but doesn't yet include Age. Now you go ahead and add Age as a predictor in addition to Compliance Rate and the other features in the model. Because the effect of Age on Failure is completely mediated by Compliance Rate, adding Age as a predictor will not help the model's accuracy, even though of course it is very much a cause of Failure. This is an example of the situation where X (Age) is a cause of Y (Failure) but doesn't help with accuracy.

To illustrate the second point, consider the following hypothetical structure:

```
Outside Workouts <- Age -> FTP
```

In this scenario, older athletes are more likely to do outside workouts and also have a lower functional threshold power (FTP). You have a model to predict FTP that doesn't include athletes' ages or how often they do outside workouts. Now a data scientist adds information about outside workouts as one of the predictors for FTP and this improves the accuracy of said prediction. Is the data scientist now licensed to conclude that doing outside workouts causes lower FTP? Of course not. Doing outside workouts is merely spuriously correlated with FTP. This is an example of a situation where X (Outside Workouts) is not a cause of Y (FTP) but still helps with predictive performance.

Machine learning won't answer our why-questions, but luckily there's an [entire scientific field](https://en.wikipedia.org/wiki/Causal_inference), namely causal inference, that is devoted to the types of methods that can be used to answer such questions. Some of the methods in the field are familiar in the context of sports science--randomized experiments, for example--but some of the methods are underutilized. With the emergence of large-scale observational datasets about endurance training, I suspect more and more researchers and companies will adopt causal inference methods to understand _why_ training plans work or don't.

## Machine learning doesn't evaluate counterfactuals

One of the hot topics in endurance training is the question of what kind of intensity distribution works best. There are two major paradigms: sweet spot training and polarized training. In sweet spot training, you spend more time in the middle of your power range, while in polarized training you avoid the middle range and spend more time at a very low or high intensity.

To evaluate the whether sweet spot training or polarized training works better for a given athlete, we need to consider two outcomes: one in which the athlete completes a sweet spot program and another in which the athlete completes a polarized program. The problem here is that an individual athlete can only complete one type of program at a time. If athlete A completes a sweet spot program and achieves a 10% increase in her FTP, we cannot say that sweet spot program is the optimal choice for A without knowing what increase she would have achieved under a polarized regime. If athlete B completes a polarized program and ends up with a 5% lower FTP, we also can't say that the polarized approach was not the optimal one for her; perhaps she would've lost even more power under a sweet spot regime.

We also can't compare the results of A and B to claim that sweet spot works better on average. Athletes A and B could be very different to begin with, and perhaps there's some general trend such that stronger athletes navigate towards sweet spot training and weaker athletes towards polarized training. That's why it's a complete non-starter to try to evaluate the effectiveness of each regime by comparing, say, the predicted FTPs or workout failure rates between polarized and sweet spot athletes.

Again, these are questions that fall squarely into the field of causal inference. If you have a model of the kinds of athlete characteristics that cause them to choose either a sweet spot program or a polarized program, you may be able to estimate the effectiveness of each type of program from purely observational data. But for training platforms like TrainerRoad, Sufferfest, Xert and others, there's a great and in my view severely underutilized alternative: the [randomized encouragement design](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2446460/). With this method, you would randomly _encourage_ athletes to adopt either a sweet spot program or a polarized program, without forcing anyone to do so. You would then use the variation in take up rates caused by the randomization as an instrument to estimate the effect of each type of training paradigm. This way, all athletes would be free to choose their preferred training approach, but you would still be able to estimate the effectiveness of the alternatives in an unbiased way. This is just one example of the ways in causal inference approaches will help to answer the most important questions in endurance training.

## Conclusion
The increasing availability of data is bound to lead to disruptions in endurance training. To speed up these disruptions, it's helpful to look beyond the standard machine learning tasks of classification and prediction. In particular, if we want to understand _why_ certain training approaches work or which training approach is optimal for a given athlete, it will be helpful to look at the field of causal inference for methods to answer these questions.
