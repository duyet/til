---
description: Pull Image from Github Docker Package Private
---

# Pull an Image from a Private Registry

## Create the Secret

```bash
kubectl create secret docker-registry <name> \
    --docker-server=docker.pkg.github.com \
    --docker-username=<github-username> \
    --docker-password=<personal-token> \
    --docker-email=<github-email>
```

```bash
kubectl create secret docker-registry <name> \
    --docker-server=docker.pkg.github.com \
    --docker-username=<github-username> \
    --docker-password=<personal-token> \
    --docker-email=<github-email>
    -o yaml > github-secret.yaml
    
# view the content
cat github-secret.yaml

# apply to k8s
kubectl apply -f github-secret.yaml
```

## Create deployment

{% code title="pod.yaml" %}
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-name
spec:
  containers:
  - name: name
    image: docker.pkg.github.com/duyet/<image-name>:latest
  imagePullSecrets:
  - name: <name>
```
{% endcode %}

Apply to k8s

```yaml
kubectl apply -f pod.yaml
```

## Reference

[https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/)

