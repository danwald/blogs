---
title: "http_referer is not accurate"
datePublished: Sat Sep 28 2024 08:21:25 GMT+0000 (Coordinated Universal Time)
cuid: cm1lvurmh00020aky1vt1dg0m
slug: httpreferer-is-not-accurate
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/MAgPyHRO0AA/upload/66c9e67c30dbb368f65f98549a2a351f.jpeg
tags: http, nginx, http-headers, referrer, referrer-policy, referer

---

The `Referer` http header (actually a [misspelling](https://en.wikipedia.org/wiki/HTTP_referer) of referrer) identifies the address of the webpage from which the resources has been requested. I wanted to add this context to an API request fired from that page.

When making the request, the value only included the host and not path of the page, which was pretty much useless for my use case.

This behavior was actually intentional and governed by our nginx server’s [policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referrer-Policy)

> `referrer-policy: origin-when-cross-origin`

which would only use the *host* since the request was to a *different* [*origin*](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) server.

This was done as a security measure. The more your know.

### Reference:

* [Referer Header](https://en.wikipedia.org/wiki/HTTP_referer)
    
* [Referrer Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referrer-Policy)
    
* [Same Origin Policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)