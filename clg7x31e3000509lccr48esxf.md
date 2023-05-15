---
title: "Minimal Viable Solution"
datePublished: Sat Apr 08 2023 11:53:15 GMT+0000 (Coordinated Universal Time)
cuid: clg7x31e3000509lccr48esxf
slug: minimal-viable-solution
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/fnUT40XljnI/upload/a820afa1e3a9cdd3bc9174b2698cf3b0.jpeg
tags: django, latency

---

One of our Django admin pages on a service kept triggering a latency alert. The engineer determined that the culprit was a dynamic field that computed a hierarchy for each record.

The proposal to remove the field was shot down by the operations team as it was vital to their work.

I asked for alternatives, to which she listed: use an external cache; denormalize the field on the entity; make the field lazy in the view, but it needed investigation;

I asked how many records are in the view, to which she stated, 100. I asked, can we simply reduce the number of records per page?

That afternoon, a config update was released to half the number of pages in the offending view.

Most of the time quick is better than perfect and simple is better/cheaper than exotic.