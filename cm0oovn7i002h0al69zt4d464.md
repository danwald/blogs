---
title: "Shorten pytest's test names"
datePublished: Thu Sep 05 2024 02:49:45 GMT+0000 (Coordinated Universal Time)
cuid: cm0oovn7i002h0al69zt4d464
slug: shorten-pytests-test-names
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/F2FcId5pz5g/upload/5298d3661fda413fc79d1e89e51d89a3.jpeg
tags: python, pytest, parameterized-tests

---

I noticed that the unittest pipeline was failing. I opened up the logs and saw a wall of text that took about 20 pages to scroll through to see what was failing. It turned out to be an `Assert` failure where the input wasn't raising an `exception`.

The parametrized test case failure was 1MB `byte` array that needed to raise the exception.

Parameterize tests need `ids` for each test, which the test case's arguments generate.

> Numbers, strings, booleans and None will have their usual string representation used in the test ID. For other objects, pytest will make a string based on the argument name:

Luckily, `parametrize` 's `ids` keyword argument takes an iterable of strings for which you can override this default behavior.

Good bye wall of text!

Reference

* [Different test options for test IDs](https://docs.pytest.org/en/latest/example/parametrize.html#different-options-for-test-ids)