# Athena - Add Partition

```sql
ALTER TABLE table_name ADD
  PARTITION (dt = '2020-01-01') 
  LOCATION 's3://mystorage/path/to/2020/01/01/'
```



**Python script:**

```python
for year in range(2017, 2020):
    for month in range(1, 13):
        for day in range(1, 32):
                print(
"""ADD PARTITION (date_index='{year}-{month}-{day}')
location "s3://data/dw/year={year}/month={month}/day={day}"
""".format(**{
            'year': str(year).zfill(4),
            'month': str(month).zfill(2),
            'day': str(day).zfill(2)
}))
```

