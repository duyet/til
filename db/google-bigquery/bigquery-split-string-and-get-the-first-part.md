# BigQuery - Split string and get the first part

Using `SPLIT(value[, delimiter])` returns an array.

Then using `SAFE_OFFSET(zero_based_offset)` or `SAFE_ORDINAL(one_based_offset)` to get item from array.

```sql
SELECT SPLIT(app_info.version, '-')[SAFE_OFFSET(0)] as app_version
FROM ...
```

References:

* [https://cloud.google.com/bigquery/docs/reference/standard-sql/string\_functions\#split](https://cloud.google.com/bigquery/docs/reference/standard-sql/string_functions#split)
* [https://cloud.google.com/bigquery/docs/reference/standard-sql/array\_functions\#safe\_offset\_and\_safe\_ordinal](https://cloud.google.com/bigquery/docs/reference/standard-sql/array_functions#safe_offset_and_safe_ordinal)

