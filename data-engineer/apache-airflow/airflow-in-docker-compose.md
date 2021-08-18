---
description: Setup Airflow in Docker Compose
---

# Airflow in Docker Compose

```yaml
# docker-compose.env

POSTGRES_USER=airflow
POSTGRES_PASSWORD=airflow
POSTGRES_DB=airflow
LOAD_EX=n
EXECUTOR=Local
AIRFLOW__CORE__DAGS_FOLDER=/opt/airflow/dags
AIRFLOW__CORE__SQL_ALCHEMY_CONN=postgresql+psycopg2://airflow:airflow@postgres:5432/airflow
AIRFLOW__CORE__FERNET_KEY=.............
```

```yaml
# docker-compose.yml

version: '2.1'

services:
    postgres:
        image: postgres:9.6
        env_file:
            - docker-compose.env
        volumes:
            - /tmp/postgres-data:/var/lib/postgresql/data

    adminer:
        image: adminer
        restart: always
        ports:
        - 9999:8080

    webserver:
        build: .
        restart: always
        depends_on:
            - postgres
        env_file:
            - docker-compose.env
        volumes:
            - ./dags:/opt/airflow/dags
            - /tmp/airflow_logs:/root/airflow/logs
        ports:
            - "8080:8080"
        command: webserver
        healthcheck:
            test: ["CMD-SHELL", "[ -f /usr/local/airflow/airflow-webserver.pid ]"]
            interval: 30s
            timeout: 30s
            retries: 3

    scheduler:
        build: .
        restart: always
        depends_on:
            - postgres
        env_file:
            - docker-compose.env
        volumes:
            - ./dags:/opt/airflow/dags
            - /tmp/airflow_logs:/root/airflow/logs
        command: scheduler
```

```ocaml
# Dockerfile

FROM duyetdev/airflow:1.10.5

ENV PYTHONPATH "/opt/airflow/dags:$PYTHONPATH"
ENV AIRFLOW_HOME "/root/airflow"

COPY . /opt/airflow
RUN pip install -r /opt/airflow/requirements.txt

# Scripts, code, ...
COPY script/auth /
COPY dags /opt/airflow/dags
```

Run:

```ocaml
docker-compose up
```

Visit: [http://localhost:8080](http://localhost:8080)

