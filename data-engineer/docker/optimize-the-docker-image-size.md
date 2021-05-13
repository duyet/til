# Optimize the Docker Image Size

## Cleaning up in the same layer

```text
FROM ubuntu:14.04
RUN apt-get update && \
    apt-get install -y curl python-pip && \
    pip install requests && \
    apt-get remove -y python-pip curl && \
    rm -rf /var/lib/apt/lists/*
ADD ./my_service.py /my_service.py
ENTRYPOINT ["python", "/my_service.py"]
```

## Apt install with \`--no-install-recommends\` 

```text
...
RUN apt-get install -y --no-install-recommends curl python-pip
...
```

## Multi-Stage Builds

```text
FROM golang:1.8-alpine as builder
RUN go get github.com/kardianos/govendor
RUN go get github.com/nicksnyder/go-i18n/goi18n
RUN go get github.com/jteeuwen/go-bindata/go-bindata
RUN make build # Exports binaries to to ./bin/$BINARY

FROM alpine
COPY --from=builder ./bin/replicated /bin/replicated
ENTRYPOINT ["/bin/replicated"]
```

