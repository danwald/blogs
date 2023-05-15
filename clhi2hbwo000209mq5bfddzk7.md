---
title: "Python's attribute look-up"
datePublished: Wed May 10 2023 19:01:44 GMT+0000 (Coordinated Universal Time)
cuid: clhi2hbwo000209mq5bfddzk7
slug: pythons-attribute-look-up
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/wstYTyWtGac/upload/ba60aa4095b50b2808127fb76900a13f.jpeg
tags: programming-blogs, python, python3, python-beginner, programming-tips

---

[`__getattribute__`](https://python-reference.readthedocs.io/en/latest/docs/dunderattr/getattribute.html) is always called for attribute lookup. However if not found, [`__getattr__`](https://docs.python.org/3/reference/datamodel.html#object.__getattr__) is called.

We can leverage this mechanism falling back to getting attributes from anything [else](https://github.com/danwald/courses/blob/master/python/attrib.py).

Below we use a `dict` for look-ups and if it's not found, raise the expected `AttributeError`

```python
import dataclasses
import logging

logging.basicConfig(level='INFO')
logger = logging.getLogger(__name__)


@dataclasses.dataclass
class DictAttrib:
    # class attribute
    name:  str
    # runtime user defined attributes  
    data:  dict = dataclasses.field(default_factory=dict)

    def __str__(self):
        return f'{self.name}| {self.data}'

    def __getattr__(self, name):
        """called when attribute not found after __getattribute__"""
        try:
            # check if in dict
            return self.data[name]
        except KeyError:
            # to avoid nested exception error
            pass
        raise AttributeError(name)


if __name__ == '__main__':
    foo = DictAttrib('foo')
    bar = DictAttrib('bar', data={'bar': 'hello'})
    try:
        logger.info(f'{foo}')
        logger.info(f'{foo.bar}')
    except AttributeError:
        logger.exception('failure')

    try:
        logger.info(f'{bar}')
        logger.info(f'{bar.bar}')
        logger.info(f'{bar.a}')
    except AttributeError:
        logger.exception('failure')
```