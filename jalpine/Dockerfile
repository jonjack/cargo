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
    mkdir /opt /opt/jre && \
    curl --progress-bar -jkSLH "Cookie: oraclelicense=accept-securebackup-cookie"\
     http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}u${JAVA_UPDATE}-b${JAVA_BUILD}/server-jre-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.tar.gz | tar -xzf - -C /opt && \
    mv /opt/jdk1.${JAVA_VERSION}.0_${JAVA_UPDATE}/jre /opt && \
    rm -rf /opt/jdk1.${JAVA_VERSION}.0_${JAVA_UPDATE} && \
    chown -R root: /opt && \
    rm -rf \
       /var/cache/apk/* \
       /opt/jre/plugin \  
       /opt/jre/lib/jfr \
       /opt/jre/lib/*jfx* \
       /opt/jre/lib/desktop \
       /opt/jre/lib/deploy* \
       /opt/jre/lib/*javafx* \
       /opt/jre/lib/javaws.jar \
       /opt/jre/lib/oblique-fonts \
       /opt/jre/lib/ext/jfxrt.jar \
       /opt/jre/lib/ext/nashorn.jar \
       /opt/jre/lib/amd64/libjfx*.so \
       /opt/jre/lib/amd64/libglass.so \    
       /opt/jre/lib/amd64/libprism_*.so \
       /opt/jre/lib/amd64/libjavafx*.so \
       /opt/jre/lib/amd64/libfxplugins.so \
       /opt/jre/lib/amd64/libdecora_sse.so \
       /opt/jre/lib/amd64/libgstreamer-lite.so \
       /opt/jre/bin/jjs \
       /opt/jre/bin/orbd \
       /opt/jre/bin/rmid \
       /opt/jre/bin/javaws \
       /opt/jre/bin/pack200 \
       /opt/jre/bin/keytool \
       /opt/jre/bin/tnameserv \
       /opt/jre/bin/unpack200 \
       /opt/jre/bin/policytool \
       /opt/jre/bin/servertool \
       /opt/jre/bin/rmiregistry && \
    apk del curl ca-certificates tar
       
ENV JAVA_HOME /opt/jre
ENV PATH ${PATH}:${JAVA_HOME}/bin
EXPOSE 80 443