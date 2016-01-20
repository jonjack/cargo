FROM jonjack/jalpine

ENV SCALA_VERSION 2.11.7

RUN echo 'http://dl-4.alpinelinux.org/alpine/v3.3/main' >> /etc/apk/repositories && \
    apk upgrade --update && \
    apk add curl tar bash && \
    curl --progress-bar -jkSL http://downloads.typesafe.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.tgz | tar -xzf - -C /opt && \
    mv /opt/scala-${SCALA_VERSION} /opt/scala && \
    chown -R root: /opt/scala && \
    rm -rf \
     /var/cache/apk/* \
     /opt/scala/man \
     /opt/scala/doc && \
    apk del curl tar && \
    apk add git

ENV SCALA_HOME /opt/scala
ENV PATH ${PATH}:${SCALA_HOME}/bin