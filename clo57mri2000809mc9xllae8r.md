---
title: "Postgres database restore via dumps"
datePublished: Wed Oct 25 2023 03:42:52 GMT+0000 (Coordinated Universal Time)
cuid: clo57mri2000809mc9xllae8r
slug: postgres-database-restore-via-dumps
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/cV9-hOgoaok/upload/e9c8410ef36b6e9266cc3761b83f4fde.jpeg
tags: database, migration, postg

---

Create the database dump (you'll be prompted for the password)

`pg_dump -U<DB_USER> -h<DB_HOST> <DB_NAME> > dumpfile`

Copy over the dump file to the new machine that has postgresql installed

Recreate the DB or drop individual tables

Apply the dump

`psql -U<DB_USER> -h<DB_HOST> -d <DB_NAME> < dumpfile`

> The dumpfile might need to be altered to be ingested into a higher versioned DB