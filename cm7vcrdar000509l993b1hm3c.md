---
title: "Replica Lag"
datePublished: Wed Mar 05 2025 03:22:50 GMT+0000 (Coordinated Universal Time)
cuid: cm7vcrdar000509l993b1hm3c
slug: replica-lag
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/RVUeAaZZNtg/upload/d088972b93681ac17a1931ff9340405f.jpeg
tags: cdn, django, metrics, databases, replication

---

Websites are inherently read heavy. There are various technologies that help to serve content from [CDNs](https://aws.amazon.com/what-is/cdn/) to application level caching. Databases can also be configured with read only [replicas](https://aws.amazon.com/rds/features/read-replicas/). Read queries can [routed](https://docs.djangoproject.com/en/5.1/topics/db/multi-db/#database-routers) to these servers alleviating the load on the master database. However, replicas can lag behind the master if

1. There are DDLs on the master that needs to be replicated
    
2. Under provisioned read replicas are trying to keep up with busy master
    

These would lead to inconsistent reads by the application. To avoid lag, one could

1. Direct all traffic to master to reduce load on replicas allowing them to catch up
    
2. Spin up a beefier Read replica before the DDL and drop lagging replicas
    

Always monitor your application and database during these updates with respective alerts setup. CPU is the only host metric that will be throttled. Breaching memory and disk space limits will result in node termination and irrecoverable application degradation, respectively.

References:

1. [What is a CDN?](https://aws.amazon.com/what-is/cdn/)
    
2. [Read Replicas](https://aws.amazon.com/rds/features/read-replicas/)
    
3. [Django’s Multi database router](https://docs.djangoproject.com/en/5.1/topics/db/multi-db/#database-routers)