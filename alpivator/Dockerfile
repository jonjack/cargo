FROM jonjack/jalpine:jdk

ENV MAJOR=1 MINOR=3 PATCH=7

RUN echo 'http://dl-4.alpinelinux.org/alpine/v3.3/main' >> /etc/apk/repositories && \
    apk upgrade --update && \
    apk add curl ca-certificates unzip bash && \
	curl --progress-bar -jkSL \
      https://downloads.typesafe.com/typesafe-activator/${MAJOR}.${MINOR}.${PATCH}/typesafe-activator-${MAJOR}.${MINOR}.${PATCH}-minimal.zip \
      -o activator-${MAJOR}.${MINOR}.${PATCH}.zip && \
      unzip -j activator-${MAJOR}.${MINOR}.${PATCH}.zip -d /opt/activator && \
      chmod 755 -R /opt/activator && \
      rm -rf \
       /var/cache/apk/* \
       activator-${MAJOR}.${MINOR}.${PATCH}.zip && \
      apk del curl ca-certificates unzip

ENV PATH ${PATH}:/opt/activator
EXPOSE 9000