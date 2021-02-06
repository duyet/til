---
description: >-
  Sometimes we need to check files in Docker build context, or just to check
  .dockerignore is work or not
---

# Checking files in Docker build context

Build this Dockerfile

```text
FROM busybox

RUN mkdir /tmp/build/
COPY . /tmp/build/
RUN du -ah tmp/build | sort -n -r | head -n 100
```

```bash
docker build .
```

