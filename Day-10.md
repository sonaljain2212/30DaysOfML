# #30daysoftechreading

Day-10/30

**Quote of the day**: If you are still believing, you are almost there!!

**Team**: If we made this change in the application, we will have more users! 
**Boss**: Can you prove it??
**Team**: How about A/B testing???

Ring a bell? No? Then read the article **“Data science you need to know! - A/B testing”** which I chose for today’s reading. 

Link: (https://towardsdatascience.com/data-science-you-need-to-know-a-b-testing-f2f12aff619a)

This article outlines A/B testing, and the steps necessary to plan and build your own robust A/B test. This article will also suit data scientists working in product development, and product managers hoping to communicate better with their data scientists.

### What is an A/B test or Randomised controlled test(RCT)?

A/B testing (also known as bucket testing or split-run testing) is a user experience research methodology. A/B tests consist of a randomized experiment with two variants, A and B. It includes application of statistical hypothesis testing or "two-sample hypothesis testing" as used in the field of statistics. A/B testing is a way to compare two versions of a single variable, typically by testing a subject's response to variant A against variant B, and determining which of the two variants is more effective.

In simple terms, An A/B test will enable us to accurately quantify our effect size and errors, and so calculate the probability that we have made a type I or type II error.

### Principles of A/B tests:

To perform a A/B test, we first need to form our question as a hypothesis, we then need to work out our randomization strategy, sample size and finally our method of measurement.

#### hypothesis
A hypothesis is a formal statement describing the relationship you want to test. A hypothesis must be a simple, clear and testable statement (more on test-ability below) that contrasts a control sample (e.g. Layout A) with a treatment sample (e.g. Layout B).

For instance, we rephrase “does an SMS system improve repayment” into two statements, a null hypothesis and an alternative hypothesis:

**Null hypothesis (H0)** : The null hypothesis usually states that there is no difference between treatment and control groups. (To put this another way, we’re saying our treatment outcome will be statistically similar to our control outcome )

**Alternative hypothesis (H1)**: The alternative hypothesis states that there is a difference between treatment and control groups.(In other words, the treatment outcome will be statistically different to the control outcome)

In other words, the Notably, a hypothesis should include reference to the population under study (Amazon.com US visitors, London bank customers etc), the intervention (website layout A and B, targeted loan repayment SMS), the comparison group (what are comparing to), the outcome (what will you measure) and the time (at what point will you measure it).

Population, Intervention, Comparison, Outcome, Time = PICOT. Remember PICOT when defining your hypotheses. 

**Randomisation**

Returning to our Amazon example, once we have a well formed hypothesis we can think about randomisation strategies. To extend our example from above, we could randomise our visitors in two ways:

- Randomly assign visitors to Layout A or B
- Allow visitors to opt-in to new layout betas

let us examine the reasons why we randomize in an A/B test. Randomization in an A/B test serves two related purposes:

- Distributing co-variates evenly
- Eliminating statistical bias


**Co-variates** are factors that might influence your outcome variable, for example, visitor geolocation, gender and risk-appetite. Note that some of these are observable and measurable (such as location and gender) and some of these are unobservable (such as risk appetite, which is difficult to measure).

**Statistical bias** can occur when your sample is substantially different from your target population. In an A/B test we are assuming our sample is representative of our population, deviations from this assumption can lead us to an incorrect understanding of our population and generating conclusions that look robust but are actually invalid!


Common forms of bias at this stage of A/B test design (which also effect our co-variate distributions) are:

**Randomization bias** — bias due to poor randomization resulting in unbalanced Treatment/Control groups (e.g. Texan visitors are over-represented in our treatment visitors vs. our control visitors). This allows some co-variates (e.g. being Texan) to exert more influence in one group than another.

**Selection bias** — bias would also result if we were to allow visitors to assign themselves to Treatment/Control groups. This is because there may be unobservable co-variates that are associated with a Treatment/Control choice. For example, visitors with more risk appetite and might select themselves into the beta testing group, and so our Treatment visitors might have both a treatment effect and a risk appetite effect

**Confounding**: Both of these will lead to what is called confounding bias, this means it will be difficult to untangle effects that are due to poor randomisation vs. effects that are due to the actual intervention.

However, if each participant has an equal chance of being randomly assigned to a Treatment/Control group then randomization will be free of bias. This will result in both observable (e.g. location) and unobservable co-variates (such as risk appetite) being spread equally to Treatment and Control groups. It is this spreading of co-variates that allows us to understand causality.

**Cluster randomisation**
Sometimes, we won’t be able to randomise at the individual level but we will still want to measure at that level. For example, if we were to randomly assess the impact of incentives for bank staff on customer loan repayment rates then it would not be possible to randomise at the customer levels (as these share banks and therefore bank staff) and we would instead need to randomise at the bank level whilst still measuring the customer level outcome (repayment rate).

The process of randomizing at one level but measuring at another causes complications in our A/B test design. Specifically, the inherent similarity of customers sharing a bank (in the above example) will lead us to have narrower distributions and under-estimate our errors. This, in turn, will have knock on effects for our study power and our study results (i.e. we’ll have a higher rate of false positives due to false confidence in our data). The concept that individuals treated in groups will behave similarly is known as clustering and our solution is to use a cluster randomized trial or cluster A/B test.

**Power**: Know your statistical power, sample size and MDE(Minimum detectable effects) before and after a trial.

**Measurement**: Measurements must be robust and reliable, think about the ways that we might be inaccurate and try to minimize the importance of self-reported metrics in any study you design!

