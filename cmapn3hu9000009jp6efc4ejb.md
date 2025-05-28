---
title: "When to use __call__"
datePublished: Thu May 15 2025 17:24:42 GMT+0000 (Coordinated Universal Time)
cuid: cmapn3hu9000009jp6efc4ejb
slug: when-to-use-call
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/-0xCCPIbl3M/upload/1fa1aa6acae161ae4ca078a5217234fb.jpeg
tags: python, oauth, oauth2, metaprogramming, pycon, requestly

---

[Requests](https://requests.readthedocs.io/en/latest/)

> `request.get(url, auth: AuthBase=obj, **kwargs)`

accepts a `obj: requests.auth.AuthBase` to attach a user’s credentials required for a [custom authentication](https://requests.readthedocs.io/en/latest/user/advanced/#custom-authentication) flow.

It [mutate's](https://github.com/danwald/butterfly/blob/main/interfaces/auth.py#L49) the `request` object to generate an [“Authorization” Header](https://github.com/danwald/butterfly/blob/main/interfaces/auth.py#L116) using the context(content) of the request itself. It uses this hook *before* making the network calling `obj(request)`

Your class needs to be a [callable](https://devdocs.io/python~3.13/reference/datamodel#object.__call__) which is done by implementing `__call__(self, *args)`. This can be used as a general hook to support esoteric use cases based on `type` of the args your class is called with. It’s a meta programming equivalent of a class decorator as describe by [this](https://www.youtube.com/watch?v=kKJR-aYew2o) insightful pyconUS talk by Aditya Mehra.

## References

* [Requests](https://requests.readthedocs.io/en/latest/)
    
* [Request’s Custom Authentication](https://requests.readthedocs.io/en/latest/user/advanced/#custom-authentication)
    
* [Python Data model object.\_\_call\_\_](https://devdocs.io/python~3.13/reference/datamodel#object.__call__)
    
* [Mutate request object for Auth](https://github.com/danwald/butterfly/blob/main/interfaces/auth.py#L49)
    
* [Metaprogramming with Decorators, Metaclasses, and Dynamic Code Generation - Aditya Mehra](https://www.youtube.com/watch?v=kKJR-aYew2o)