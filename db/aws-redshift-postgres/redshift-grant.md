# Redshift - GRANT

Grant all on schema to user\_name:

```sql
GRANT ALL
ON SCHEMA schema_name
TO user_name;


GRANT ALL PRIVILEGES
ON ALL TABLES IN SCHEMA schema_name
TO user_name;
```



```sql
-- Grant Usage permission to Read-Only Group to specific Schema
GRANT USAGE ON SCHEMA "ro_schema" TO GROUP ro_group;

-- Grant Select permission to Read-Only Group to specific Schema
GRANT SELECT ON ALL TABLES IN SCHEMA "ro_schema" TO GROUP ro_group;
```

Change owner:

```sql
ALTER TABLE
    <schema>.<table> OWNER TO <user>;
```



