# Useful SQL queries for Apache Airflow

## Get tasks run

```sql
SELECT * 
FROM task_instance
WHERE 
    dag_id LIKE 'abc%' 
    AND task_id != 'start'
    AND execution_date >= '2020-04-20';
```

## Delete tasks run to trigger backfill

```sql
BEGIN;

    DELETE 
    FROM task_instance
    WHERE 
        dag_id LIKE 'abc%' 
        AND task_id != 'start'
        AND execution_date >= '2020-04-20';
    
    SELECT 1;
COMMIT;
```

