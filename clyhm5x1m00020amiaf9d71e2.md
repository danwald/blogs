---
title: "Filter PII"
datePublished: Thu Jul 11 2024 18:39:58 GMT+0000 (Coordinated Universal Time)
cuid: clyhm5x1m00020amiaf9d71e2
slug: filter-pii
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/uAzUg6_tMCo/upload/983b0b283b2fda543105ee837e9a626f.jpeg
tags: python, security, privacy, pii

---

[Python Logging](https://docs.python.org/3/howto/logging.html) is a centralized place to filter out sensitive Personally Identifiable Information.

The flow chart shows how a [LogRecord](https://docs.python.org/3/library/logging.html#logging.LogRecord) propagates through the logging frameworks' layers. We can leverage the [`Filter`](https://web.archive.org/web/20201130054012/https://wtanaka.com/node/8201) layer (over the `formatter`) to redact information.

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720490510414/d86cc536-7295-4073-b79d-f73a2793fbf7.png align="center")](https://docs.python.org/3/howto/logging.html#logging-flow)

You can use the convenient [Loggingredactor](https://pypi.org/project/loggingredactor/) library to do so. The redaction acts on

* `record.msg` which is the format `str` line that's match across regex patterns
    
* `record.args` are any parameters that's passed to the log which are interpolated against the format string `msg`. This checks any dictionary for keys that needs to be redacted.
    

```python
def filter(self, record):
    try:
        record.msg, record.args = (
            self.redact(record.msg), self.redact(deepcopy(record.args)
        )
    except Exception:
        pass
    return True
```

> `deepcopy` to not mutate the shared (by reference) args object
> 
> Always logs content by returning `True`

[Wesley's Page](https://web.archive.org/web/20201130054012/https://wtanaka.com/node/8201) provides some nice example of the popular [python-json-logger](https://github.com/madzak/python-json-logger)

### References

* [https://docs.python.org/3/howto/logging.html](https://docs.python.org/3/howto/logging.html)
    
* [https://docs.python.org/3/library/logging.html#logging.LogRecord](https://docs.python.org/3/library/logging.html#logging.LogRecord)
    
* [https://docs.python.org/3/library/logging.html#filter-objects](https://docs.python.org/3/library/logging.html#filter-objects)
    
* [https://relaxdiego.com/2014/07/logging-in-python.html](https://relaxdiego.com/2014/07/logging-in-python.html)
    
* [https://betterstack.com/community/guides/logging/sensitive-data/](https://betterstack.com/community/guides/logging/sensitive-data/)
    
* [https://pypi.org/project/loggingredactor/](https://pypi.org/project/loggingredactor/)
    
* [https://web.archive.org/web/20201130054012/https://wtanaka.com/node/8201](https://web.archive.org/web/20201130054012/https://wtanaka.com/node/8201)
    
* [https://github.com/madzak/python-json-logger](https://github.com/madzak/python-json-logger)