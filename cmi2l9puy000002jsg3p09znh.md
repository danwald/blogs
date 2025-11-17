---
title: "1+N querys"
datePublished: Mon Nov 17 2025 03:32:29 GMT+0000 (Coordinated Universal Time)
cuid: cmi2l9puy000002jsg3p09znh
slug: 1n-querys
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/5Pln0OGhrvc/upload/746733fb75070d475a02a515b8fb02b2.jpeg
tags: python, django, databases, query-optimization

---

Widely know as N+plus one problem, it’s actually a misnomer. As [@](https://bsky.app/profile/adamj.eu)[adamj.eu](http://adamj.eu)’s [article](https://adamj.eu/tech/2020/09/01/django-and-the-n-plus-one-queries-problem/) neatly summarize with examples (and now my dyslexic mind actually understands it), it’s one query to get a list of N objects that you iterate over. And each iteration is a query as the initial query is lazy evaluated.

To avoid this in django, use:

1. [select\_related](https://docs.djangoproject.com/en/5.2/ref/models/querysets/#select-related) (for one-to-one or one-to-many queries)
    
2. [prefetch\_related](https://docs.djangoproject.com/en/5.2/ref/models/querysets/#prefetch-related) (for many-to-many, many-to-one or generic-relations queries)
    

where it gets the related rows with the initial query, as the name indicates.

*Always try and minimize the queries to a shared resource.*

Happy hackin’

### [Referen](https://bsky.app/profile/adamj.eu)ces:

* [Article: django and the n plus one queries problem](https://adamj.eu/tech/2020/09/01/django-and-the-n-plus-one-queries-problem/)
    
* [Django: QuerySet:prefetch\_related](https://docs.djangoproject.com/en/5.2/ref/models/querysets/#prefetch-related)