---
description: Get all S3 Keys by Prefix by Boto3
---

# get\_all\_s3\_keys

```python
def scan_s3_objects(bucket, prefix):
    """
    Get a list of all keys in an S3 bucket.

    Args:
        - bucket: S3 bucket name
        - prefix: S3 prefix to be scanned
    Returns:
        - List of objects.
    """
    s3 = boto3.client('s3')
    keys = []

    kwargs = {'Bucket': bucket, 'Prefix': prefix}
    while True:
        resp = s3.list_objects_v2(**kwargs)
        if 'Contents' not in resp:
            return []

        for obj in resp['Contents']:
            keys.append(obj['Key'])

        try:
            kwargs['ContinuationToken'] = resp['NextContinuationToken']
        except KeyError:
            break

    return keys
```



