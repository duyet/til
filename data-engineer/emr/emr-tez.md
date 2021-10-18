---
description: Upscale/Downscale of the emr cluster corrupts hdfs jars /apps/tez/tez.tar.gz
---

# EMR - Tez

## Solution 1:

Repair the **tez.tar.gz** file and increase replication value

```
wget https://downloads.apache.org/tez/0.9.2/apache-tez-0.9.2-bin.tar.gz
tar -zxvf apache-tez-0.9.2-bin.tar.gz
hadoop fs -rm /apps/tez/tez.tar.gz
hadoop fs -copyFromLocal apache-tez-0.9.2-bin/share/tez.tar.gz /apps/tez/
hadoop fs -setrep -w 3 /apps/tez/
```

## Solution 2:

Referring the tar file directly from S3

{% code title="tez-site.xml" %}
```
tez.lib.uris=s3://bucketName/tez/tez.tar.gz
```
{% endcode %}
