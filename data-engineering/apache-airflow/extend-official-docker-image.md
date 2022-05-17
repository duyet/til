# Extend official Docker image

```docker
FROM apache/airflow:2.3.0

# Add apt package for python packages the required extra c++ libs, ...
USER root
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
         vim openjdk-11-jre-headless \
  && apt-get autoremove -yqq --purge \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
  
ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64

# Install custom python libs
USER airflow
RUN pip install --no-cache-dir lxml apache-airflow-providers-apache-spark==2.1.3

# Embed DAGs code into docker
COPY --chown=airflow:root ./dags /opt/airflow/dags
```



Ref: [https://airflow.apache.org/docs/docker-stack/build.html#adding-new-apt-package](https://airflow.apache.org/docs/docker-stack/build.html#adding-new-apt-package)
