---
title: "Python's all docs are misleading"
datePublished: Sat Sep 21 2024 11:48:06 GMT+0000 (Coordinated Universal Time)
cuid: cm1c35lh4000a08k0f0fh0qgk
slug: pythons-all-docs-are-misleading
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/PDxYfXVlK2M/upload/55e5d6723d70683d3f5072c71ecb5228.jpeg
tags: python, generators, logic, boolean, iterable

---

Going by the documentation for [all](https://docs.python.org/3/library/functions.html#all), one would think all iterables will early return.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1726917593050/ca5946c3-c3e3-41d3-85dd-2fb4c6cb64a0.png align="center")

The following code will throw an `AttributeError` on the last item of the list iteratable.

```python
def bad_all(o: object, att: str, l: list):
    if all([o is not None, getattr(o, att, None) in l]):
        return True
    return False
```

The subtlety here is since we’re using a **list** above, it will evaluate *each* item of the list first and not chain the logic as we expect to early return, resulting in the error.

Chain your logic explicitly using booleans to avoid this …

> `if o and getattr(o, att, None) in l:`

… or use lazy generators which will early return.

Be sure to avoid some other python [gotchas](https://docs.python-guide.org/writing/gotchas/) too.

### References:

* [Python’s all documentation](https://docs.python.org/3/library/functions.html#all)
    
* [Python Gotchas](https://docs.python-guide.org/writing/gotchas/)