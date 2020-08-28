# Create public Helm chart repository with GitHub Pages

## 1. Create Helm Chart repo

Sample: [https://github.com/duyet/charts](https://github.com/duyet/charts)

![](../../.gitbook/assets/image%20%281%29.png)

## 2. Chart testing and linting

[https://github.com/duyet/charts/blob/master/.github/workflows/helm-template-validation.yml](https://github.com/duyet/charts/blob/master/.github/workflows/helm-template-validation.yml)

```yaml
name: Helm Template Validation

on: [push, pull_request]

jobs:
  chart-lint:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
      
    - name: Fetch history
      run: git fetch --prune --unshallow
      
    - name: Run chart-testing (lint)
      id: lint
      uses: helm/chart-testing-action@v1.0.0-rc.1
      with:
        config: .github/ct-lint.yaml
        command: lint

    - name: Create kind cluster
      uses: helm/kind-action@v1.0.0-alpha.3
      # Only build a kind cluster if there are chart changes to test.
      if: steps.lint.outputs.changed == 'true'

    - name: Run chart-testing (install)
      uses: helm/chart-testing-action@v1.0.0-rc.1
      with:
        config: .github/ct-install.yaml 
        command: install
```

## 3. Build helm chart

```bash
# helm package <chartname>/*
helm package amundsen/*
helm package spark-shuffle-service/*

# Successfully packaged chart and saved it to: ./amundsen-1.0.0.tgz
# Successfully packaged chart and saved it to: ./spark-shuffle-0.1.0.tgz
```

**Create the Helm chart repository index**

According to [Helm](https://helm.sh/docs/developing_charts/):

> A repository is characterized primarily by the presence of a special file called `index.yaml` that has a list of all of the packages supplied by the repository, together with metadata that allows retrieving and verifying those packages.

{% tabs %}
{% tab title="Bash" %}
```bash
helm repo index --url https://duyet.github.io/charts .
```
{% endtab %}

{% tab title="cat index.yaml" %}
```yaml
apiVersion: v1
entries:
  amundsen:
  - apiVersion: v1
    created: "2020-08-28T15:52:17.747491+07:00"
    dependencies:
    - condition: elasticsearch.enabled
      name: elasticsearch
      repository: https://kubernetes-charts.storage.googleapis.com/
      version: 1.32.5
    description: Amundsen is a metadata driven application for improving the productivity
      of data analysts, data scientists and engineers when interacting with data.
    digest: 92a30cb7c9e6523d277464eb381d0c96de5e496416270735283ba0a150a8c924
    home: https://github.com/lyft/amundsen
    icon: https://github.com/lyft/amundsen/blob/master/docs/img/logos/amundsen_logo_on_light.svg
    keywords:
    - metadata
    - data
    - amundsen
    maintainers:
    - email: me@duyet.net
      name: Duyet Le
    name: amundsen
    sources:
    - https://github.com/lyft/amundsen
    - https://github.com/duyet/charts/amundsen
    urls:
    - https://duyet.github.io/charts/amundsen-1.0.0.tgz
    version: 1.0.0
  - apiVersion: v1
    created: "2020-08-28T15:52:17.754643+07:00"
    dependencies:
    - condition: elasticsearch.enabled
      name: elasticsearch
      repository: https://kubernetes-charts.storage.googleapis.com/
      version: 1.32.5
    description: Amundsen is a metadata driven application for improving the productivity
      of data analysts, data scientists and engineers when interacting with data.
    digest: b0cfdb0a9add154134299c72da8ff005da5686f6181b869820e046aafd8ef58e
    home: https://github.com/lyft/amundsen
    icon: https://github.com/lyft/amundsen/blob/master/docs/img/logos/amundsen_logo_on_light.svg
    keywords:
    - metadata
    - data
    - amundsen
    maintainers:
    - email: me@duyet.net
      name: Duyet Le
    name: amundsen
    sources:
    - https://github.com/lyft/amundsen
    - https://github.com/duyet/charts/amundsen
    urls:
    - https://duyet.github.io/charts/.dist/amundsen-1.0.0.tgz
    version: 1.0.0
  spark-shuffle:
  - apiVersion: v1
    appVersion: "1.0"
    created: "2020-08-28T15:52:17.748015+07:00"
    description: A Helm chart to deploy Spark shuffle service deamon set for Kubernetes
    digest: 1da1d6b7f6121f2aefba4073974df472b2ce337433edd79a7cf2a1d799dee618
    home: https://github.com/duyet/charts/tree/master/spark-shuffle-service
    maintainers:
    - email: me@duyet.net
      name: duyet
      url: https://github.com/duyet/
    name: spark-shuffle
    urls:
    - https://duyet.github.io/charts/spark-shuffle-0.1.0.tgz
    version: 0.1.0
generated: "2020-08-28T15:52:17.741837+07:00"

```
{% endtab %}
{% endtabs %}

Automated to scan and build helm in subfolders:

{% code title="build.sh" %}
```bash
#!/bin/bash
set -x

for chart in ./*; do
    if [ -f "$chart/Chart.yaml" ]; then
        helm package $chart
    fi
done

helm repo index --url https://duyet.github.io/charts .
```
{% endcode %}

## 4. Public helm chart

You can commit the helm package to the `master` branch, then public all content by Github pages.

![Settings &amp;gt; Github Pages](../../.gitbook/assets/image%20%283%29.png)

##  5. Github Workflows Action for build and publish

```yaml
name: Publish helm packages

on:
  push:
    branches:
    - release

jobs:
  chart-lint-and-build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2

    - name: Fetch history
      run: git fetch --prune --unshallow

    - name: Run chart-testing (lint)
      id: lint
      uses: helm/chart-testing-action@v1.0.0-rc.1
      with:
        config: .github/ct-lint.yaml
        command: lint

    - name: Create kind cluster
      uses: helm/kind-action@v1.0.0-alpha.3
      # Only build a kind cluster if there are chart changes to test.
      if: steps.lint.outputs.changed == 'true'

    - name: Run chart-testing (install)
      uses: helm/chart-testing-action@v1.0.0-rc.1
      with:
        config: .github/ct-install.yaml
        command: install

    - name: Helm build packages
      run: ./build.sh
```

## 6. **Configure helm client for testing**

```yaml
$ helm repo add duyet https://duyet.github.io/charts/
# “duyet” has been added to your repositories
```

**Test the Helm chart repository**

```text
$ helm search commento
NAME CHART VERSION APP VERSION DESCRIPTION
[…]
duyet/commento 0.1.0 1.0 A Helm chart for Kubernetes
[…]
```



