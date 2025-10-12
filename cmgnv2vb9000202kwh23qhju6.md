---
title: "Alembic disables my logs"
datePublished: Sun Oct 12 2025 15:30:51 GMT+0000 (Coordinated Universal Time)
cuid: cmgnv2vb9000202kwh23qhju6
slug: alembic-disables-my-logs
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/UsET4S0ginw/upload/4f335b40102ea45e7b69988e80c92799.jpeg
tags: python, logging, flask-sqlalchemy, alembic, missing

---

**…and how to get them back**

Alembic is SQLAlchemy's database migration framework—think change management for your relational database. It autogenerates scripts tracking your ORM model changes, letting you recreate your data model at any point in time.

Most apps run migrations on startup. I noticed my logs would mysteriously vanish right after the migration check.

The culprit? This innocent-looking snippet in the auto-generated [`env.py`](http://env.py):

```python
if config.config_file_name is not None:
    fileConfig(config.config_file_name)
```

That `fileConfig` defaults to `disable_existing_loggers=True` (thanks, [backwards compatibility!](https://docs.python.org/3/library/logging.config.html#logging.config.fileConfig)), nuking any logging you previously configured.

**The fix:** Either edit the generated [`env.py`](http://env.py) or configure your logging *after* migrations run.

Happy hackin'

### References:

* [Stackoverflow article](https://stackoverflow.com/questions/78780118/how-can-i-stop-the-alembic-logger-from-deactivating-my-own-loggers-after-using-a)
    
* [Alembic](https://alembic.sqlalchemy.org/en/latest/)
    
* [SQLAlchemy](https://www.sqlalchemy.org/)
    
* [loggging.config.fileConfig](https://docs.python.org/3/library/logging.config.html#logging.config.fileConfig)