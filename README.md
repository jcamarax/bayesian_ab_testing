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


## Statistical modelling
To run the A/B test, the two populations of study are the:
- control group : gorup of users that have only seen the PSA.
- test group : group of users that have seen the advertisement from the marketing company.
  
The two metrics that will be analysed are the total ads and the conversion rate. Both will be assumed to be two random variables, meaning that the values are generated from a random process that will be modelised by statistical distributions.

Most of the time, the normal distribution $` X \sim N(\mu,\sigma^2) `$ is used to describe metrics of a data analysis, without being realised. This distribution is great, indeed, because it is well know and has great properties (such as $`E[X] = \mu `$, $` VAR[X] = \sigma `$ and an estimator of $`\mu`$ is the arithmetic mean )   without considering the nature of the data. However, this law describes continuous random variables and not discrete random variables such as the total ads and conversation rate. For example, the binomial distribution $` X \sim B(n,p)`$ would probably better suited for the totals ads. Assuming the marketing campaign is run over a period of 30 days (n = 30) and asses whether each day the user has seen the ad (Yes or No question). So p would describe the propability that that a user see an ad on an aday (and 1-p the opposite)! As for the convertion rate, a simple bernouilli distribution would do the job $`X \sim B(p)`$, with p the proportion of people that brought the product after seing the ad!

Note that to run the statistical tests, it will be assumed that all the users from a group belongs to the same statistical population. This is important to note because it means that two users from a group is assumed to have the same behaviour. In reality, it might be an assumption far from reality. Indeed, the behaviour from each user might come from a unique random process different from all to each other (that's why we need to watch for those outlier values!). But, for to run the A/B test, this assumption has to be made unless proven to be wrong.

The statistical that I will use is the 2-sample t-test to compare the total ads seen by t

## Results 
1. Frequentist approach
2. Bayesian approach

## Conclusion

## Source
[1] [A/B testing, optimizely](https://www.optimizely.com/optimization-glossary/ab-testing/)
[2] [Kaggle Marketing A/B Testing datasets, faviofazquez user](https://www.kaggle.com/datasets/faviovaz/marketing-ab-testing/data)
