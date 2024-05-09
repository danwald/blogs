---
title: "Chained celery tasks with delay"
datePublished: Thu May 09 2024 01:38:56 GMT+0000 (Coordinated Universal Time)
cuid: clvyky6x1000109k0hbse8rq8
slug: chained-celery-tasks-with-delay
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/iJg1YzsEfqo/upload/a77855d858313f06098771aa72379100.jpeg
tags: async, celery, task, celery-chain

---

Leverage [Celery Chains](https://docs.celeryq.dev/en/stable/userguide/canvas.html#chains) to execute sequential tasks. But it wasn't clear from the documentation on how to add a delay in-between executions.

The initial (reasonable) attempt:

```python
result = (
  add.s(1,1) |
  mul.s(3) | 
  mul.s(4)
).apply_async(countdown=5)  # 24
```

resulted in the task completing immediately.

However setting the `countdown` for each signature\* worked.

```python
result = (
  add.s(1,1) | 
  mul.s(3).set(countdown=5) | 
  mul.s(4).set(countdown=5)
) # 24
```

> \*use [immutable signatures](https://docs.celeryq.dev/en/stable/userguide/canvas.html#immutability) (shortcut: si) so the next task doesn't require the return value of the previous one who's result is implicitly passed as the first argument