# Postgres - List tables

### Using psql

```bash
\dt
```

```bash
# \dt
             List of relations
 Schema |     Name      | Type  |  Owner
--------+---------------+-------+----------
 public | actor         | table | postgres
 public | address       | table | postgres
 public | category      | table | postgres
 ....
```

### Using pg\_catalog schema

```sql
SELECT
   *
FROM
   pg_catalog.pg_tables
WHERE
   schemaname != 'pg_catalog'
AND schemaname != 'information_schema';
```

Reference:

* [http://www.postgresqltutorial.com/postgresql-show-tables/](http://www.postgresqltutorial.com/postgresql-show-tables/)

