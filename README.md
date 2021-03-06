# docker-alpine-gradle

Gradle for multi-stage docker image build.

Dockerfile [ci-and-cd/docker-alpine-gradle on Github](https://github.com/ci-and-cd/docker-alpine-gradle)

[cirepo/gradle on Docker Hub](https://hub.docker.com/r/cirepo/gradle/)

## Use this image as a “stage” in multi-stage builds

```dockerfile

FROM alpine:3.9

COPY --from=cirepo/glibc:2.29-r0-alpine-3.9-archive /data/root /
COPY --from=cirepo/java-11-openjdk:11.0.2-alpine-3.9-archive /data/root/usr/lib/jvm/java-11-openjdk /usr/lib/jvm/java-11-openjdk
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk

COPY --from=cirepo/gradle:5.2.1-alpine-archive /data/root /
ENV GRADLE_HOME /opt/gradle
ENV PATH ${JAVA_HOME}/bin:${GRADLE_HOME}/bin:${PATH}

```
