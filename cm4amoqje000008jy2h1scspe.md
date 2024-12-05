---
title: "DevX: Time to merge"
datePublished: Thu Dec 05 2024 01:18:26 GMT+0000 (Coordinated Universal Time)
cuid: cm4amoqje000008jy2h1scspe
slug: devx-time-to-merge
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/nShLC-WruxQ/upload/0f7fab13f3920cf54ce39b2ae5a43220.jpeg
tags: productivity, git, devx, devex

---

There are several frameworks available to help understand and improve **Dev**eloper e**X**perience at organizations. They collect metrics along serval dimensions.

The [SPACE](https://queue.acm.org/detail.cfm?id=3454124) framework looks along the lines of: **S**atisfaction/Well-being; **P**roductivity; **A**ctivity; **C**ommunication/Collaboration; **E**fficiency/Flow.

We are measuring *Activity* and *Communication*. Specifically we are measuring the *number of merges* and *merge times* respectfully across our repositories.

To get quarterly merge times of Pull Requests into main, [this](https://github.com/danwald/devX/blob/main/git-stats/merge-stats.sh) script does the heavy lifting analyzing local repositories using command-line `git` and a `python` one-liner to get the timing statistics (average, min, max and median).

We are only considering PRs which are sluggish. We ignoring the quick ones which are under a week and the stale ones which are over a month. The goal is to reduce these numbers while maintaining our quality metrics.

It’s been running for close to a quarter and will report back on the results, but in the meantime have at it.

### References

* [SPACE framework](https://queue.acm.org/detail.cfm?id=3454124)
    
* [Measure What Matter’s](https://www.whatmatters.com/the-book)
    
* [Merge Times Script](https://github.com/danwald/devX/blob/main/git-stats/merge-stats.sh)