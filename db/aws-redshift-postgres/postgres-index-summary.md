# Postgres - Index Summary

Here's a sample query to pull the number of rows, indexes, and some info about those indexes for each table. Ditch the pg_size_pretty if you’re on an ancient (<= 8.2) version)

```sql
SELECT
    pg_class.relname,
    pg_size_pretty(pg_class.reltuples::bigint) AS rows_in_bytes,
    pg_class.reltuples AS num_rows,
    count(indexname) AS number_of_indexes,
    CASE WHEN x.is_unique = 1 THEN 'Y'
       ELSE 'N'
    END AS UNIQUE,
    SUM(case WHEN number_of_columns = 1 THEN 1
              ELSE 0
            END) AS single_column,
    SUM(case WHEN number_of_columns IS NULL THEN 0
             WHEN number_of_columns = 1 THEN 0
             ELSE 1
           END) AS multi_column
FROM pg_namespace 
LEFT OUTER JOIN pg_class ON pg_namespace.oid = pg_class.relnamespace
LEFT OUTER JOIN
       (SELECT indrelid,
           max(CAST(indisunique AS integer)) AS is_unique
       FROM pg_index
       GROUP BY indrelid) x
       ON pg_class.oid = x.indrelid
LEFT OUTER JOIN
    ( SELECT c.relname AS ctablename, ipg.relname AS indexname, x.indnatts AS number_of_columns FROM pg_index x
           JOIN pg_class c ON c.oid = x.indrelid
           JOIN pg_class ipg ON ipg.oid = x.indexrelid  )
    AS foo
    ON pg_class.relname = foo.ctablename
WHERE 
     pg_namespace.nspname='public'
AND  pg_class.relkind = 'r'
GROUP BY pg_class.relname, pg_class.reltuples, x.is_unique
ORDER BY 2;
```

Source: [https://wiki.postgresql.org/wiki/Index_Maintenance](https://wiki.postgresql.org/wiki/Index_Maintenance)
