FROM alpine

ENV NODE_VERSION=5.5.0 NPM_VERSION=3.6.0

RUN apk upgrade --update && \
  apk add curl gnupg make gcc g++ python linux-headers paxctl libgcc libstdc++ && \
  curl -SLO https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}.tar.gz && \
  curl -SLO https://nodejs.org/dist/v${NODE_VERSION}/SHASUMS256.txt.asc && \
  set -ex \
  && for key in \
    9554F04D7259F04124DE6B476D5A82AC7E37093B \
    94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
    0034A06D9D9B0064CE8ADF6BF1747F4AD2306D93 \
    FD3A5288F042B6850C66B31F09FE44734EB7990E \
    71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
    DD8F2338BAE7501E3DD5AC78C273792F7D83545D \
  ; do \
    gpg --keyserver hkp://http-keys.gnupg.net:80 --recv-keys "$key"; \
  done && \
  gpg --verify SHASUMS256.txt.asc && \
  grep "node-v${NODE_VERSION}.tar.gz\$" SHASUMS256.txt.asc | sha256sum -c - && \

  tar -xzf "node-v${NODE_VERSION}.tar.gz" && \
    cd /node-v${NODE_VERSION} && \
      ./configure --prefix=/usr && \
      make -j$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
      make install && \
      paxctl -cm /usr/bin/node && \
      cd / && \
      if [ -x /usr/bin/npm ]; then \
        npm install -g npm@${NPM_VERSION} && \
        find /usr/lib/node_modules/npm -name test -o -name .bin -type d | xargs rm -rf; \
      fi && \
      apk del curl gnupg make gcc g++ python linux-headers paxctl && \
      rm -rf /node-v${NODE_VERSION} /node-v${NODE_VERSION}.tar.gz /SHASUMS256.txt.asc \
      /usr/lib/node_modules/npm/html \
      /usr/lib/node_modules/npm/man \
      /usr/lib/node_modules/npm/doc \
      /root/.npm /root/.node-gyp /etc/ssl /tmp/* /usr/share/man /var/cache/apk/* \
      /root/.gnupg/pubring.kbx

EXPOSE 80 8080