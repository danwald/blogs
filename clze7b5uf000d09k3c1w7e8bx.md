---
title: "Don't mutate your paginated query_sets"
datePublished: Sat Aug 03 2024 14:00:32 GMT+0000 (Coordinated Universal Time)
cuid: clze7b5uf000d09k3c1w7e8bx
slug: dont-mutate-your-paginated-querysets
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/5IHz5WhosQE/upload/a8981e8960ad958bb6a96d323cb7148c.jpeg
tags: django, mutations, query, offset

---

Django's Paginator works to batch your query items into pages. Under the hood it uses lazy slicing which is accomplished in sql by `offset` and `limit`.

> **Warning** altering the `data` affects the limit/offset of proceeding paginated pages

```python
data               = [1,2,3,4,5,6,7,8,9,10]
data_in_pages      = [(1,2),(3,4),(5,6),(7,8),(9,10)]
limit_offset_pages = [[0,2],[2,2],[4,2],[6,2],[8,2]] #zero index

for limit, offset in limit_offset_pages:
    sliver = data[limit:limit+offset]
    for index, item in enumerate(sliver, start=limit):
        if not item % 2: # delete even numbers
            del data[index]
```

As an alternative take the top slice of your mutated queryset to guarantee nothing will be missed.

```python
while items:=query_set()[:batch_size]:
    process_items(items) #mutator 
```

*Never get high (mutate) on your own supply.*

### References

* [Django's Paginator](https://docs.djangoproject.com/en/5.0/topics/pagination/)
    
* [Postgresql's Offset/limit](https://www.postgresql.org/docs/current/queries-limit.html)