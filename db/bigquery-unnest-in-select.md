# Bigquery - UNNEST in SELECT

```sql
SELECT 
    event_name,
    (SELECT value.int_value FROM UNNEST(event_params) WHERE key = "value") as score,
FROM `example_*`
```

