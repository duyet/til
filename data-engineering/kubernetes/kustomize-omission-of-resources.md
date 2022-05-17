---
description: 'Skip one of the resources, adding `$path: delete` kustomize will skip it.'
---

# Kustomize: omission of resources

```yaml
apiVersion: v1
kind: Service
metadata:
  name: some-public-service
$patch: delete
```

Source: [https://github.com/kubernetes-sigs/kustomize/issues/106](https://github.com/kubernetes-sigs/kustomize/issues/106)
