---
title: "Missing initial migration"
datePublished: Fri Jan 23 2026 16:56:26 GMT+0000 (Coordinated Universal Time)
cuid: cmkr4hnyc000x02kzemtl0p0y
slug: missing-initial-migration
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/h5ZqVoCDgys/upload/865d211a4a31e036cb5778acf6c95231.jpeg
tags: flask, database-migrations

---

Using the [Flask-Migrate](https://pypi.org/project/Flask-Migrate/) extension you can create database migrations for your application.

Flask application’s typically auto-create db tables on start

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1768907722395/103e2b9b-d0ba-4107-8cb1-158676d11cac.png align="center")

So running `flask db upgrade` you’ll get:

> `INFO [alembic.env] No changes in schema detected.`

To create the initial migration, override the applications existing database with a temporary memory-based one

> `DATABASE_URL=sqlite:/// flask db migrate`

Happy hackin’!

### References

* Flask-Migrate: [Documentation](https://flask-migrate.readthedocs.io/)
    
* Alembic: [Cookbook - Building an Up to Date Database from Scratch](https://alembic.sqlalchemy.org/en/latest/cookbook.html)
    
* Miguel Grinberg: [How To Add Flask-Migrate To An Existing Project](https://blog.miguelgrinberg.com/post/how-to-add-flask-migrate-to-an-existing-project)