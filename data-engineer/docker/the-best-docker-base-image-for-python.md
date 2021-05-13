# The best Docker base image for Python

## Optimized size

**The official Docker Python image in its slim variant—e.g. `python:3.9-slim-buster`—is a good base image for most use cases.** it’s 41MB to download, 114MB when uncompressed to disk, it gives you the latest Python releases, it’s easy to use and it’s got all the benefits of Debian Buster.

## Optimized performance

**If you care about performance, you’ll want to use `ubuntu:20.04`.** Having [run some benchmarks comparing multiple Python builds](https://pythonspeed.com/articles/faster-python/), it turns out that switching to Ubuntu 20.04 can give you a 20% performance boost. As such, if Python performance matters to you, I would recommend using the `ubuntu:20.04` image. It’s a bit more annoying to set up, and for some reason gets updates less often, but it will be faster.  


Ref: [https://pythonspeed.com/articles/base-image-python-docker-images/](https://pythonspeed.com/articles/base-image-python-docker-images/)

