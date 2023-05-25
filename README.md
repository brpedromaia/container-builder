# Openbox VNC Lightweight Container

## Synopsis

Buildah & Podman Container designed for CI container builds.

### Gitlab CI Simple usage
```yaml
Container_Build:
  image: brpedromaia/container-builder
  stage: Assembly
  before_script:
    - podman login --tls-verify=false -u ${CI_REGISTRY_USER} -p ${CI_REGISTRY_PASSWORD} $CI_REGISTRY
  script:
    - podman build -t ${CONTAINER_IMAGE_URL} --build-arg FROM_IMAGE_URL=${FROM_IMAGE_URL} -f $CONTAINER_FILE $CONTAINER_CONTEXT
    - podman push --tls-verify=false ${CONTAINER_IMAGE_URL}
  variables:
    CONTAINER_IMAGE_URL: "${CI_REGISTRY}/${CI_PROJECT_NAMESPACE}/${CI_PROJECT_NAME}:${CI_PIPELINE_ID}"
    CONTAINER_FILE: "ContainerFile"
    CONTAINER_CONTEXT: "."
```
