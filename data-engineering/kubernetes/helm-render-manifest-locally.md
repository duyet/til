# Helm: render manifest locally

1. Install yq (`brew install yq`)
2. Download chart to local
3. Get values from release yaml
4. Using `helm template` to render manifest

```bash
function download {
  CHART_REPO=$(yq r ${1} spec.chart.repository)
  CHART_NAME=$(yq r ${1} spec.chart.name)
  CHART_VERSION=$(yq r ${1} spec.chart.version)
  CHART_DIR=${2}/${CHART_NAME}
  helm repo add ${CHART_NAME} ${CHART_REPO}
  helm fetch --version ${CHART_VERSION} --untar ${CHART_NAME}/${CHART_NAME} --untardir ${2}
  echo ${CHART_DIR}
}

HELM_RELEASE=my-release
TMPDIR=/tmp/${HELM_RELEASE}

# Download chart to local
CHART_DIR=$(download ${HELM_RELEASE} ${TMPDIR}| tail -n1)

# Custom values
yq r ./releases/$HELM_RELEASE.yaml spec.values > my-custom.values.yaml

HELM_RELEASE_NAME=$(yq r ${HELM_RELEASE} metadata.name)
HELM_RELEASE_NAMESPACE=$(yq r ${HELM_RELEASE} metadata.namespace)

# Render 
helm template ${HELM_RELEASE_NAME} ${CHART_DIR} --namespace $HELM_RELEASE_NAMESPACE --skip-crds true -f my-custom.values.yaml
```

Ref: [https://github.com/stefanprodan/hrval-action/blob/master/src/hrval.sh](https://github.com/stefanprodan/hrval-action/blob/master/src/hrval.sh)
