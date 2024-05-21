---
title: "`LIKE` uses a range index"
datePublished: Tue May 21 2024 02:01:27 GMT+0000 (Coordinated Universal Time)
cuid: clwfr1drh000209md1e7c9xvp
slug: like-uses-a-range-index
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/Q9y3LRuuxmg/upload/92a1e5e1def53ed19edecf087e5554e8.jpeg
tags: mysql, django, sql, index, query-optimization

---

A Django's Auth table's indexes:

```bash
mysql> show index from auth_user;

+-----------+------------+------------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+

| Table     | Non_unique | Key_name   | Seq_in_index | Column_name | Collation | Cardinality | Sub_part | Packed | Null | Index_type | Comment | Index_comment |

+-----------+------------+------------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+

| auth_user |          0 | PRIMARY    |            1 | id          | A         |         130 |     NULL | NULL   |      | BTREE      |         |               |

| auth_user |          0 | email      |            1 | email       | A         |         130 |     NULL | NULL   |      | BTREE      |         |               |

| auth_user |          0 | username   |            1 | username    | A         |         130 |     NULL | NULL   |      | BTREE      |         |               |

| auth_user |          1 | is_active  |            1 | is_active   | A         |           2 |     NULL | NULL   |      | BTREE      |         |               |

+-----------+------------+------------+--------------+-------------+-----------+-------------+----------+--------+------+------------+---------+---------------+

4 rows in set (0.01 sec)
```

where a search by the exact email

> `select * from auth_user where email = 'foo@bar.com';`

results in:

> `const` search on the `email` index

[`const`](https://dev.mysql.com/doc/refman/8.0/en/explain-output.html#jointype_const) *tables are very fast because they are read only once.\**

```bash
+----+-------------+-----------+------------+-------+---------------+-------+---------+------+------+----------+--------+

| id | select_type | table     | partitions | type  | possible_keys | key   | key_len | ref   | rows | filtered | Extra |

+----+-------------+-----------+------------+-------+---------------+-------+---------+-------+------+----------+-------+

|  1 | SIMPLE      | auth_user | NULL       | const | email         | email | 227     | const |    1 |   100.00 | NULL  |

+----+-------------+-----------+------------+-------+---------------+-------+---------+-------+------+----------+-------+
```

While a prefix scan using `like` (it's done by default in django admin panels)

> `select * from auth_user where email LIKE 'foo@bar.com';`

results in:

> a `range` search used on the `email` index. Using Index Condition Push down optimization\*\* (ICP).

ICP conditionally reads a table row to match other conditions in the where clause iff the indexed column is a match.

In search by the exact email case, it's almost equivalent to the `const` search above. In both cases the whole index was scanned.

```bash
+----+-------------+-----------+------------+-------+---------------+-------+---------+------+------+----------+-----------------------+

| id | select_type | table     | partitions | type  | possible_keys | key   | key_len | ref  | rows | filtered | Extra                 |

+----+-------------+-----------+------------+-------+---------------+-------+---------+------+------+----------+-----------------------+

|  1 | SIMPLE      | auth_user | NULL       | range | email         | email | 227     | NULL |    1 |   100.00 | Using index condition |

+----+-------------+-----------+------------+-------+---------------+-------+---------+------+------+----------+-----------------------+
```

The edge belongs to the exact match search which uses const tables.

### References:

\*[MySQL's - Explain output](https://dev.mysql.com/doc/refman/8.0/en/explain-output.html);

\*\*[Index Condition Push Down Optimzation](https://dev.mysql.com/doc/refman/8.0/en/index-condition-pushdown-optimization.html);