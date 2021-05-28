# BigQuery - UNNEST in SELECT

We can use `UNNEST` in the nested fields, rather than unnesting in the WHERE clause and JOIN

```sql
SELECT 
    event_name,
    (SELECT value.int_value FROM UNNEST(event_params) WHERE key = "value") as score,
FROM `example_*`
```

