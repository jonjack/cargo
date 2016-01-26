FROM alpine

ENV JAVA_VERSION=8 JAVA_UPDATE=72 JAVA_BUILD=15

RUN echo 'http://dl-4.alpinelinux.org/alpine/v3.3/main' >> /etc/apk/repositories && \
    apk upgrade --update && \
    apk add curl ca-certificates tar && \
    curl --progress-bar -o glibc-2.21-r2.apk https://circle-artifacts.com/gh/andyshinn/alpine-pkg-glibc/6/artifacts/0/home/ubuntu/alpine-pkg-glibc/packages/x86_64/glibc-2.21-r2.apk && \
    curl --progress-bar -o glibc-bin-2.21-r2.apk https://circle-artifacts.com/gh/andyshinn/alpine-pkg-glibc/6/artifacts/0/home/ubuntu/alpine-pkg-glibc/packages/x86_64/glibc-bin-2.21-r2.apk && \
    apk add --allow-untrusted glibc-2.21-r2.apk glibc-bin-2.21-r2.apk && \
    /usr/glibc/usr/bin/ldconfig /lib /usr/glibc/usr/lib && \
    rm glibc-2.21-r2.apk glibc-bin-2.21-r2.apk && \
    echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf && \
    mkdir /opt && \
    curl --progress-bar -jkSLH "Cookie: oraclelicense=accept-securebackup-cookie"\
     http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}u${JAVA_UPDATE}-b${JAVA_BUILD}/jdk-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.tar.gz | tar -xzf - -C /opt && \
    mv /opt/jdk1.${JAVA_VERSION}.0_${JAVA_UPDATE}/ /opt/jdk/ && \
    chown -R root: /opt && \
    rm -rf \
       /var/cache/apk/* \
       /opt/jdk/javafx-src.zip \  
       /opt/jdk/src.zip \
       /opt/jdk/db \
       /opt/jdk/man \
       /opt/jdk/lib/missioncontrol \
       /opt/jdk/lib/visualvm \
       /opt/jdk/jre/plugin \  
       /opt/jdk/jre/lib/jfr \
       /opt/jdk/jre/lib/*jfx* \
       /opt/jdk/jre/lib/desktop \
       /opt/jdk/jre/lib/deploy* \
       /opt/jdk/jre/lib/*javafx* \
       /opt/jdk/jre/lib/javaws.jar \
       /opt/jdk/jre/lib/oblique-fonts \
       /opt/jdk/jre/lib/ext/jfxrt.jar \
       /opt/jdk/jre/lib/ext/nashorn.jar \
       /opt/jdk/jre/lib/amd64/libjfx*.so \
       /opt/jdk/jre/lib/amd64/lib*cms.so \
       /opt/jdk/jre/lib/amd64/libglass.so \    
       /opt/jdk/jre/lib/amd64/libprism_*.so \
       /opt/jdk/jre/lib/amd64/libjavafx*.so \
       /opt/jdk/jre/lib/amd64/libfxplugins.so \
       /opt/jdk/jre/lib/amd64/libdecora_sse.so \
       /opt/jdk/jre/lib/amd64/libgstreamer-lite.so \
       /opt/jdk/jre/bin/jjs \
       /opt/jdk/jre/bin/orbd \
       /opt/jdk/jre/bin/rmid \
       /opt/jdk/jre/bin/javaws \
       /opt/jdk/jre/bin/pack200 \
       /opt/jdk/jre/bin/keytool \
       /opt/jdk/jre/bin/tnameserv \
       /opt/jdk/jre/bin/unpack200 \
       /opt/jdk/jre/bin/policytool \
       /opt/jdk/jre/bin/servertool \
       /opt/jdk/jre/bin/rmiregistry && \
    apk del curl ca-certificates tar
       
ENV JAVA_HOME /opt/jdk
ENV PATH ${PATH}:${JAVA_HOME}/bin
EXPOSE 80 443