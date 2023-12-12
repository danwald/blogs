---
title: "Prod DB CPU spike via testcode"
datePublished: Tue Dec 12 2023 17:28:33 GMT+0000 (Coordinated Universal Time)
cuid: clq2m9hch000609jubyqx5vfj
slug: prod-db-cpu-spike-via-testcode
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/dBI_My696Rk/upload/280a1e4b0f028bdfcc4364c86bd92b06.jpeg
tags: web-development, databases, debugging

---

Our test code APIs for our End-to-End tests can't be accessed in production

There was a release that added more unitests before the spike. Looking at the PR with thought nothing of it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1700068812317/d3a6089c-365f-4eec-9347-57af8187fee1.png align="center")

What we later found out was that it resulted in 100% CPU utilization.

This was due to ...

1. An existing bug in a factory that would eagerly create records when the module was loaded.
    
2. The new code loaded the buggy module when the application started due to an import dependency.
    
3. We run 100s processes (pods\*#process/pod) for the application, this table was filling up with test data.
    
4. These extra records exaggerated the inefficient data integrity queries that were run on the save of related entities, which were a lot.
    

Mitigation/Fixes:

* We stopped incoming updates (blacklist APIs, stop background updates) to the DB however, the load didn't subside.
    
* We noticed that the table with slow/high throughput queries was growing in number when it shouldn't have.
    
* We validated that it wasn't a security concern but noticed that the test code was being executed via our ELK logs.
    
* Reverted the last change and bulk deleted the newly created test records that were introduced.
    

Takeaways

* Occam's razor applies: the last change was the culprit, which we were slow to adopt.
    
* The call was chaotic and lacked leadership.
    
    * We should have orchestrated the engineering efforts more effectively and methodically.
        
    * We should have facilitated clearer reporting of findings to improve visibility.
        
* We (almost) have Isolated test code from production deployments.