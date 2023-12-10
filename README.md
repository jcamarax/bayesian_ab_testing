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


## Results 
1. Frequentist approach
2. Bayesian approach

## Conclusion

## Source
[1] [A/B testing, optimizely](https://www.optimizely.com/optimization-glossary/ab-testing/)
[2] [Kaggle Marketing A/B Testing datasets, faviofazquez user](https://www.kaggle.com/datasets/faviovaz/marketing-ab-testing/data)
