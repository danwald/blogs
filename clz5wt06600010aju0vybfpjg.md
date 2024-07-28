---
title: "Z-Scores in anomaly detection FTW"
datePublished: Sun Jul 28 2024 18:44:19 GMT+0000 (Coordinated Universal Time)
cuid: clz5wt06600010aju0vybfpjg
slug: z-scores-in-anomaly-detection-ftw
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/wA7saRSTNS8/upload/d3713cc9b181de3a1fda72485d7eaf7d.jpeg
tags: statistics, slack, cicd-cjy1vtdk2005kjjs17n8couc3, anomaly-detection

---

Before [Slack](https://slack.engineering/the-scary-thing-about-automating-deploys/?utm_source=blog.quastor.org&utm_medium=newsletter&utm_campaign=how-slack-automates-deploys) moved to release bot they used to have human deployment commanders work in 2 hour shifts to walk through deployment steps and monitor metrics for anomalies. This was their [CI/CD](https://en.wikipedia.org/wiki/CI/CD).

The main reasons why people follow CD is to *manage risk* with smaller, isolated changes allowing for *faster shipping* of features which can be iterated on based on customer traction providing a competitive edge.

To determine an anomaly, a z-score was calculated.

`z-score = (datapoint - mean) / std-dev`

> datapoint - new datapoint
> 
> mean/std-dev : previous datapoints

*number of datapoints determines window size example: last hour*

Standard deviation measure variance which is how far a datapoint is from the norm. Being the divisor, it indicates the magnitude of deviation from the previous samples. +/- 3 is a good indicator that something changed.

To reduce false positives which commonly occur with static thresholds, they use dynamic thresholds with historical data. Larger window sizes of several hours from the previous day and week, are used to compute an average. If more than 5 datapoints breach the historical average, the they need to take a look at it.

### References

* [Slack Release bot architecture](https://slack.engineering/the-scary-thing-about-automating-deploys/?utm_source=blog.quastor.org&utm_medium=newsletter&utm_campaign=how-slack-automates-deploys)
    
* [CI/CD](https://en.wikipedia.org/wiki/CI/CD)