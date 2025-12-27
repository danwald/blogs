---
title: "Gevent celery config I/O bound"
datePublished: Sat Dec 27 2025 09:16:16 GMT+0000 (Coordinated Universal Time)
cuid: cmjo35w56000002ie5atu0hvs
slug: gevent-celery-config-io-bound
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/iixVGC2dagw/upload/de16333e64d6b22b27e02560a79fa72d.jpeg
tags: python, async, event-loop, threading

---

When **NOT** using Gevent ([worker\_pool](https://docs.celeryq.dev/en/latest/userguide/configuration.html#worker-pool)\=\[prefork|gthread\]), the number of [concurrent workers](https://docs.celeryq.dev/en/latest/userguide/configuration.html#worker-concurrency) defaults to the number of cores which are effectively the tasks that will be executing in “[parallel](https://bytebytego.com/guides/concurrency-is-not-parallelism/)”.

[The prefetch multiplier](https://docs.celeryq.dev/en/latest/userguide/configuration.html#worker-prefetch-multiplier) (default 4) is an optimization to reduce round trips to the broker (queue), to eagerly fetch tasks at the node per available worker. This happens at the consumers not at the workers.

With 4 workers:

* 16 tasks consumed
    
* 12 are *waiting* for an available worker
    
* 4 are being concurrently processed
    

If you have short lived tasks this isn’t a problem. However if your workloads’ **execution time varies**, all task could potentially convoy on the same node and dramatically **reducing the throughput per worker**. It’s recommended to use a prefetch of 1 or 2 to reduce the effect.

If you strictly have [IO bound](https://en.wikipedia.org/wiki/I/O_bound) tasks you should use [gevent](https://docs.celeryq.dev/en/v5.5.3/userguide/concurrency/gevent.html). Using cooperative multitasking via a coroutine mechanism, you can effectively have 100s of workers per worker which will all execute concurrently.

Some considerations:

* Use connection pooling for database or http access to avoid herding
    
* monkey patch correctly
    
* if the workload isn’t IO bound, you will run into issues with the [GIL](https://wiki.python.org/moin/GlobalInterpreterLock).
    

Since python 3.14, [free threaded python is officially supported (phase 2)](https://docs.python.org/3.14/whatsnew/3.14.html#whatsnew314-free-threaded-now-supported). However it’s not production ready but it brings thread level parallelism to applications.

Happy Hackin’

### References:

* [worker\_pool](https://docs.celeryq.dev/en/latest/userguide/configuration.html#worker-pool)
    
* [worker\_concurrency](https://docs.celeryq.dev/en/latest/userguide/configuration.html#worker-concurrency)
    
* [Concurrency vs Parallelism](https://bytebytego.com/guides/concurrency-is-not-parallelism/)
    
* [worker\_prefetch\_multiplier](https://docs.celeryq.dev/en/latest/userguide/configuration.html#worker-prefetch-multiplier)
    
* [IO bound tasks](https://en.wikipedia.org/wiki/I/O_bound)
    
* [Gevent](https://docs.celeryq.dev/en/v5.5.3/userguide/concurrency/gevent.html)
    
* [GIL](https://wiki.python.org/moin/GlobalInterpreterLock)
    
* [Python free threads](https://docs.python.org/3.14/whatsnew/3.14.html#whatsnew314-free-threaded-now-supported)
    
* [Anthony Shaw’s talk on parallelism with python (sub-interpreters / free threads)](https://www.youtube.com/watch?v=Mp5wKOL4L2Q)