# An application of bayesian tools for A/B testing on marketing campaign
An application of bayesian tools to study user behaviour after seeing an ad 

## Table of contents
1. [Context](#table-of-contents)
2. [Introduction to bayesian inference](#introduction-to-bayesian-inference)

## Context
This work is to present an application of bayesian tools to help companies make decisions based on their current assumptions about their data (prior knowledge). When a new functionnality of a digital product is launched into production, it is to normally to target specific gains : better UX, click rate, more sales, and so on. One common test used widely is the A/B testing. A/B testing  is a methodology for comparing two versions of a webpage or app against each other to determine which one performs better [1].

After the control and test groups are defined, data have been collected, a statistical test is usully performed to assess if whether or not a stastifical difference exists between the two groups. In my experience, the test used the most is is the 2 sample t-test (for parametric distributions). It is generally assumed that the performance indicator being used is normally distributed and that the variance of the two groups being compared are similar. In practical, I've seen many instances where data analysts skip this crucial step. Indeed, they would only calculate if the p-value (threshold for statistical significance) is below 0.05 without even checking the alternative hypotesis from the t-test (means are not equals, control group mean > test group mean or control group mean < test group mean mean)! Note that there are other 2 sample test for the mean that are non parametric and that can be used for A/B testing :). If you  need guidance on this specific topic, feel free to contact me!

However, the approach desibred above is part of what is called frequentist statistics 📉.  Those methods having been used for decades but when it comes to statistical modelling, bayesian statistics is more suited (in my opinion). In this project, I will compare both approaches to answer the following questions : 
The dataset that will be usd is from a marketing campaign that aims to answer those questions :

- Would the campaign be successful?
- If the campaign was successful, how much of that success could be attributed to the ads?


## Dataset information
The dataset that will be used contains the following information : 
- Index: Row index
- user id: User ID (unique)
- test group: If "ad" the person saw the advertisement, if "psa" they only saw the public service announcement
- converted: If a person bought the product then True, else is False
- total ads: Amount of ads seen by person
- most ads day: Day that the person saw the biggest amount of ads
- most ads hour: Hour of day that the person saw the biggest amount of ads


## Statistical modelling and assumptions
To run the A/B test, the two populations of intetest are the:

- control group : gorup of users that have only seen the PSA.
- test group : group of users that have seen the advertisement from the marketing company.
  
Note that to run the statistical tests, it will be assumed that all the users from a group belongs to the same statistical population. This is important to mention because it means that two users from a group is assumed to have the same behaviour. In reality, it might be an assumption far from reality. Indeed, the behaviour from each user might come from a different random process different from all to each other s(that's why we need to watch for those outlier values and multimodal distributions... ⚠️). But, for running the A/B test, this assumption has to be made unless proven to be wrong. Another way of explaining this, let's assume I check in January the amounts of ads that user A saw: 500 views. In the following months, user A sees 450, 550, 475, 525 views. What do you think? It seems that the behaviour seems to following a pattern, right? I were surveying user B from the same population, we would get similar views. Here, we don't need to use machine learning to predict how many more views user A or B will get in the following month. This is why we do statistical modelling, to find the best distribution that will describe the behaviour of our sample! Isn't it great?

Additionnally, it is important to make the distinction between randomized control trials (RCT) and observationnal studies. In 1948, the first randomized controlled clinical trial was carried out to test a new drug (streptomycin) against pulmonary tuberculosis. Today, this type of trial is still a gold standard in modern medecine that achieves the highest level of evidence to prove a causal relationship. Therefore, we want to answer this question : If I take this new drug, will I get a positive response against pulmonary tuberculosis?  Also, in this type of trials, the sample is "randomized" to make sure that regardless of the characteristics of the participants (age, sex, health history,...), the new drug will have an effect that is not placebo. As you see, the statistician in charge will generally some spend time elaborating the best sampling strategy in his clinical trials (accounting also for confounding variables). However, in the real world, outside of clinical trials,  we will fall into into the other category of experiments which are observationnal studies. It is much simpler to explain, we "just" collect the data. But can we prove a causal relationship with this approach? Does statistical significance means causality? Unfortunately, unless you're very lucky or the guru of causality (Judea Pearls), you'll always be uncertain if your app/web new functionnality will activate or retain more users. So how do we do? Causal bayesian inference seems to be one way of demonstrating causality using observational studies. However, they're not very easy and requires to identify all the variables that can influence directly/indirectly your conclusion (it requires scientific knowledge). It doesn't mean that doing A/B testing without doing causal inference is wrong, it just means that there'll will always be some level of uncertainty on the causal relation to be evidenced (or not). To sum up this paragraph, my intention here was to raise awareness for data analysts performing A/B testing. A/B testing is a great tool but they need to keep in mind all the assumptions.

In this git project, I will just keep  itsimple and do a classic A/B testing (observaitonal study). The two metrics that will be analysed are the total ads and the conversion rate. Both will be assumed to be two random variables, meaning that the values are generated from a random process. When we do statistical inference, one the tasks is to modelize this random process with well known and simple statistical models (Normal, Exponential, Bernouilli, ...).

Most of the time, the normal distribution $` X \sim N(\mu,\sigma^2) `$ is used to describe metrics of a data analysis, without being realised. This distribution is great, indeed, because it is well known and has great properties (such as $`E[X] = \mu `$, $` VAR[X] = \sigma `$ and an estimator of $`\mu`$ is the arithmetic mean )   without considering the nature of the data. However, this law describes continuous random variables and not discrete random variables such as the total ads and conversation rate. For example, the binomial distribution $` X \sim B(n,p)`$ would probably better suited for the totals ads. Assuming the marketing campaign is run over a period of 30 days (n = 30) and asses whether each day the user has seen the ad (Yes or No question). So p would describe the propability that that a user see an ad on an aday (and 1-p the opposite)! As for the convertion rate, a simple bernouilli distribution would do the job $`X \sim B(p)`$, with p the proportion of people that brought the product after seing the ad! However, finding a good estimator of the true $` p`$ parameters from both distributions can be a challenge using standard frequentist approach (maximum likelihood estimotor,...). This is where bayesian statistics comes handy!

In this github project, I will use two approaches to perform A/B testing to check if the users significantly saw more advertisements than PSA.
In the frequentist approach, I will fit a normal distribution to the total ads seen by the two groups.
In the bayesian approach, I will fit a binomial distribution to the totals ads seen by the two groups.

## Results 
1. Frequentist approach
2. Bayesian approach

## Conclusions

## Source
[1] [A/B testing, optimizely](https://www.optimizely.com/optimization-glossary/ab-testing/)
[2] [Kaggle Marketing A/B Testing datasets, faviofazquez user](https://www.kaggle.com/datasets/faviovaz/marketing-ab-testing/data)
[3] [Controlled randomized clinical trials](https://pubmed.ncbi.nlm.nih.gov/18225427/#:~:text=However%2C%20it%20is%20the%20development,from%20those%20of%20a%20placebo.)
