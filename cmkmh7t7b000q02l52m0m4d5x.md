---
title: "Ors & Ands"
datePublished: Tue Jan 20 2026 10:53:50 GMT+0000 (Coordinated Universal Time)
cuid: cmkmh7t7b000q02l52m0m4d5x
slug: ors-and-ands
tags: python, logic, boolean, operators

---

I came across [Stephen Grupetta’s](https://x.com/s_gruppetta) [article](https://www.thepythoncodingstack.com/p/do-you-really-know-how-or-and-and-work-in-python) that highlights a nuance that I didn’t consider. `or` and `and` *don't* return booleans. They return one of their operands which can be any data type.

### The Rules

`or`:

* Returns the first operand when it's truthy
    
* Returns the second operand when the first is falsy
    

`and`:

* Returns the first operand when it's falsy
    
* Returns the second operand when the first is truthy
    

Python objects are either truthy or falsy, it doesn't matter that `or` and `and` don't return Booleans! Leverage this to short circuit on assignment for idiomatic code and avoid a [gotcha](https://docs.python-guide.org/writing/gotchas/#mutable-default-arguments)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1768269342753/0d14e3d3-6ed2-40f7-8c3f-ffb9c5af4846.png align="center")

Happy Hackin’

## References

* [**Stephen Gruppetta on X**](https://x.com/s_gruppetta)
    
* [The Python Coding Stack: Do You Really Know How `or` And `and` Work in Python?](https://www.thepythoncodingstack.com/p/do-you-really-know-how-or-and-and-work-in-python)
    
* [Python Docs: Truth Value Testing](https://docs.python.org/3/library/stdtypes.html#truth-value-testing)
    
* [Python Docs: Boolean Operations](https://docs.python.org/3/library/stdtypes.html#boolean-operations-and-or-not)
    
* [Python Gotchas: Mutable default Arguments](https://docs.python-guide.org/writing/gotchas/#mutable-default-arguments)