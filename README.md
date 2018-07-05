# docker-alpine-gradle

Gradle for multi-stage docker image build.

Dockerfile [ci-and-cd/docker-alpine-gradle on Github](https://github.com/ci-and-cd/docker-alpine-gradle)

[cirepo/alpine-gradle on Docker Hub](https://hub.docker.com/r/cirepo/alpine-gradle/)

## Use this image as a “stage” in multi-stage builds

```dockerfile

FROM alpine:3.7

COPY --from=cirepo/alpine-glibc:3.7_2.23-r3-archive /data/root /
COPY --from=cirepo/java-oracle:8u171-archive /data/root/usr/lib/jvm/java-8-oracle /usr/lib/jvm/java-8-oracle
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

COPY --from=cirepo/alpine-gradle:4.7-archive /data/root /
ENV GRADLE_HOME /opt/gradle
ENV PATH ${JAVA_HOME}/bin:${GRADLE_HOME}/bin:${PATH}

```
