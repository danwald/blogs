---
title: "frozen sets pay no heed to order"
datePublished: Sun Jul 28 2024 17:18:03 GMT+0000 (Coordinated Universal Time)
cuid: clz5tq22w000509jzgu6sak8c
slug: frozen-sets-pay-no-heed-to-order
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/x70z3qCNBuk/upload/b554fa444ed02d97cf1274aea3ee2308.jpeg
tags: python, sets

---

I superficially assumed a `frozenset` accounts for the order of items it was constructed with such that the following assertion would fail.

```bash
assert(
   frozenset([('a',1), ('b',1)]) == frozenset([('b',1), ('a',1)])
)
```

Thinking about it for a second, sets are unordered, hence the above assertion holds.