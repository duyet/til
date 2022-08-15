# env from ConfigMap or Secrets

```yaml
envFrom:
  - configMapRef:
      name: production-settings
  - configMapRef:
      name: my-app-settings
env:
  - name: S3_BUCKET
    valueFrom:
      configMapKeyRef:
        name: s3-settings
        key: bucket
```
