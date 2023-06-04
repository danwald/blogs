---
title: "Application Load Balancer service upgrades"
datePublished: Sun Jun 04 2023 17:26:56 GMT+0000 (Coordinated Universal Time)
cuid: clihp3pei000j09jl0pw70oie
slug: application-load-balancer-service-upgrades
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/902vnYeoWS4/upload/c3d4f151c6180166fcd8cf2d1015d6a6.jpeg
tags: devops, load-balancing, aws-applicaction-load-balancer

---

There were three servers under an application load balancer (ALB) that needed to be vertically scaled by our devops team. These servers were responsible for routing traffic to the website.

Servers were going to be upgraded one at a time: provisioning a new instance, adding them to the ALB; and pulling out the older one (leaving them alive long enough for connections to naturally close).

However, there were some 502s with this approach because as soon as instances were added to the ALB they received traffic while they were initializing and not really ready for it.

To avoid this, you could wait for a warmup period long enough to ensure the server is ready or set them to [slow start mode](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-target-groups.html#slow-start-mode).