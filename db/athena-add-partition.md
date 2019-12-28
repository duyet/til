# Athena - Add Partition

```sql
ALTER TABLE table_name ADD
  PARTITION (dt = '2020-01-01') 
  LOCATION 's3://mystorage/path/to/2020/01/01/'
```



**Python script:**

{% tabs %}
{% tab title="python" %}
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
{% endtab %}

{% tab title="output" %}
```sql
ADD PARTITION (date_index='2019-01-01') location "s3://data/dw/year=2019/month=01/day=01"
ADD PARTITION (date_index='2019-01-02') location "s3://data/dw/year=2019/month=01/day=02"
ADD PARTITION (date_index='2019-01-03') location "s3://data/dw/year=2019/month=01/day=03"
ADD PARTITION (date_index='2019-01-04') location "s3://data/dw/year=2019/month=01/day=04"
....
```
{% endtab %}
{% endtabs %}





