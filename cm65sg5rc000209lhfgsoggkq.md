---
title: "Dependent breaking pytest's"
datePublished: Tue Jan 21 2025 01:20:18 GMT+0000 (Coordinated Universal Time)
cuid: cm65sg5rc000209lhfgsoggkq
slug: dependent-breaking-pytests
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/s56H08cAlM0/upload/3f20358029c701360e5952fad4798344.jpeg
tags: unit-testing, python, pytest

---

New unit-tests were added that were passing when run in isolation. They were breaking when run all together by the CI/CD pipeline. Previous tests were affecting ours. The question was which ones? We thought it could be a data issue with persistent data affecting tests. However we use `@pytest.mark.django_db` which

> will set up the Django databases the first time a test needs them. Once setup, the database is cached to be used for all subsequent tests and rolls back transactions, to isolate tests from each other.

We could replicate the failure locally. Finding the breaking test case by the process of elimination, we ran test cases directories in order. Removing a directory each time while the error persisted.

The breaking test case didn't reconnect a [post\_save signal](https://docs.djangoproject.com/en/5.1/ref/signals/#post-save)’s receiver. Our tests relied on receivers. Reverting this line, and muting the firing of the signal for other failing tests we got it to work.

Moral: leave things better than you found it or at the very least, the same.

### References

* [Pytest’s database access](https://pytest-django.readthedocs.io/en/latest/database.html)
    
* [Django’s post\_save signals](https://docs.djangoproject.com/en/5.1/ref/signals/#post-save)