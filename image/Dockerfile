
FROM cirepo/nix:2.2.1-alpine-3.9


USER root


ARG IMAGE_ARG_FILESERVER
ARG IMAGE_ARG_GRADLE_VERSION


COPY --from=cirepo/glibc:2.29-r0-alpine-3.9-archive /data/root /
COPY --from=cirepo/java-11-openjdk:11.0.2-alpine-3.9-archive /data/root/usr/lib/jvm/java-11-openjdk /usr/lib/jvm/java-11-openjdk
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk


COPY --chown=root:root docker /data


RUN set -ex \
  && GRADLE_ARCH=gradle-${IMAGE_ARG_GRADLE_VERSION:-5.2.1}-bin.zip \
  && if [[ ! -f /data/${GRADLE_ARCH} ]]; then \
       ${ARIA2C_DOWNLOAD} -d /data -o ${GRADLE_ARCH} \
       ${IMAGE_ARG_FILESERVER:-https://downloads.gradle.org}/distributions/${GRADLE_ARCH}; \
     fi \
  && unzip /data/${GRADLE_ARCH} \
  && mkdir -p /opt \
  && mv gradle-${IMAGE_ARG_GRADLE_VERSION:-5.2.1} /opt/ \
  && ln -sf /opt/gradle-${IMAGE_ARG_GRADLE_VERSION:-5.2.1} /opt/gradle \
  && rm -f /data/${GRADLE_ARCH}


USER alpine


ENV GRADLE_HOME /opt/gradle
ENV PATH ${JAVA_HOME}/bin:${GRADLE_HOME}/bin:${PATH}
