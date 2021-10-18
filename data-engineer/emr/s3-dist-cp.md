---
description: >-
  Using S3DistCp, you can efficiently copy large amounts of data from Amazon
  S3/HDFS into S3/HDFS
---

# S3 Dist CP

```
s3-dist-cp -Dmapreduce.job.reduces=100 \
    -Dfs.s3a.access.key=yourAccessKey \
    -Dfs.s3a.secret.key=yourSecretKey\
    -Dmapreduce.reduce.maxattempts=3 \
    --outputManifest manifest-checkpoint.gz \
    --s3Endpoint=s3.us-east-1.amazonaws.com --src=s3a://source_s3/ --dest=s3a://dest_s3/
```

`yourAccessKey` and `yourSecretKey` should have access to both S3 source and destination.

References: [https://docs.aws.amazon.com/emr/latest/ReleaseGuide/UsingEMR_s3distcp.html](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/UsingEMR_s3distcp.html)
