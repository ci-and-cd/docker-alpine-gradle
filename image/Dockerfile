
FROM cirepo/nix:2.0.4_alpine-3.7


USER root


ARG IMAGE_ARG_GRADLE_VERSION


COPY --from=cirepo/alpine-glibc:3.7_2.23-r3-archive /data/root /
COPY --from=cirepo/java-8-oracle:8u171-archive /data/root/usr/lib/jvm/java-8-oracle /usr/lib/jvm/java-8-oracle
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle


COPY --chown=root:root docker /data


RUN set -ex \
  && if [ ! -f /data/gradle-${IMAGE_ARG_GRADLE_VERSION:-4.7}-bin.zip ]; then \
       ${ARIA2C_DOWNLOAD} -d /data -o gradle-${IMAGE_ARG_GRADLE_VERSION:-4.7}-bin.zip \
       ${IMAGE_ARG_FILESERVER:-https://downloads.gradle.org}/distributions/gradle-${IMAGE_ARG_GRADLE_VERSION:-4.7}-bin.zip; \
     fi \
  && unzip /data/gradle-${IMAGE_ARG_GRADLE_VERSION:-4.7}-bin.zip \
  && mkdir /opt \
  && mv gradle-${IMAGE_ARG_GRADLE_VERSION:-4.7} /opt/ \
  && ln -sf /opt/gradle-${IMAGE_ARG_GRADLE_VERSION:-4.7} /opt/gradle \
  && rm -f /data/gradle-${IMAGE_ARG_GRADLE_VERSION:-4.7}-bin.zip


USER alpine


ENV GRADLE_HOME /opt/gradle
ENV PATH ${JAVA_HOME}/bin:${GRADLE_HOME}/bin:${PATH}
