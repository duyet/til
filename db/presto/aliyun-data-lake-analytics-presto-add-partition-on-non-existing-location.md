# Aliyun Data Lake Analytics \(Presto\) - Add partition on non-existing location

By default, you will get the error when trying to add partition references to a non-existing oss path.

The table property `auto.create.location` will help to resolve this error. 

Examples are as follows:

```sql
​CREATE EXTERNAL TABLE person (
    `id` int,
    `name` string,
    `age` int    
)
STORED AS TEXTFILE
LOCATION 'oss://bucket001/dir001/'
TBLPROPERTIES (
    'auto.create.location'='true'
);​
```

Reference: [https://help.aliyun.com/document\_detail/193719.html](https://help.aliyun.com/document_detail/193719.html?spm=a2c4g.11186623.6.645.275170f2iZsneL)

