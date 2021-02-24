# Build a maven project with buildpacks

## Simple, no binding

    pack build demo:0.0.1-SNAPSHOT --builder=paketobuildpacks/builder:0.1.64-base

## With ca-certificates binding

```shell
pack build demo:0.0.1-SNAPSHOT \
  --env SERVICE_BINDING_ROOT=/platform/bindings \
  --volume $PWD/binding/ca-certificates/:/platform/bindings/my-certificates \
  --builder=paketobuildpacks/builder:0.1.64-base
```


## With settings.xml binding

```shell
pack build demo:0.0.1-SNAPSHOT \
  --env BP_MAVEN_BUILD_ARGUMENTS="-Dmirror-password=XXX package -DskipTests" \
  --env SERVICE_BINDING_ROOT=/platform/bindings \
  --volume $PWD/binding/maven-settings:/platform/bindings/maven-settings \
  --volume $PWD/binding/ca-certificates/:/platform/bindings/my-certificates \
  --builder=paketobuildpacks/builder:base \
  --buildpack=paketobuildpacks/builder:0.1.64-base
```
    
## With both binding AND adoptopenjdk

```shell
pack build demo:0.0.1-SNAPSHOT \
  --env BP_MAVEN_BUILD_ARGUMENTS="-Dmirror-password=XXX package -DskipTests" \
  --env SERVICE_BINDING_ROOT=/platform/bindings \
  --volume $PWD/binding/maven-settings:/platform/bindings/maven-settings \
  --builder=paketobuildpacks/builder:0.1.64-base
```
