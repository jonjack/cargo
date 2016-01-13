FROM alpine

ENV NGINX_VERSION=1.9.7 NGINX_HOME=/app/nginx

RUN echo 'http://dl-4.alpinelinux.org/alpine/v3.3/main' >> /etc/apk/repositories && \
    apk upgrade --update && \
    apk add curl gnupg openssl-dev pcre-dev build-base && \
    curl -SLO http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz && \
    curl -SLO http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz.asc && \
    set -ex \
    && for key in \
      4C2C85E705DC730833990C38A9376139A524C53E \
      7338973069ED3F443F4D37DFA64FD5B17ADB39A8 \
      65506C02EFC250F1B7A3D694ECF0E90B2C172083 \
      6E067260B83DCF2CA93C566F518509686C7E5E82 \
      B0F4253373F8F6F510D42178520A9993A1C052F8 \
      A09CD539B8BB8CBE96E82BDFABD4D3B3F5806B4D \
      573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62 \
    ; do \
      gpg --keyserver hkp://http-keys.gnupg.net:80 --recv-keys "$key"; \
    done && \
    gpg --verify nginx-${NGINX_VERSION}.tar.gz.asc nginx-${NGINX_VERSION}.tar.gz && \
    tar -xzf nginx-${NGINX_VERSION}.tar.gz && \
    cd nginx-${NGINX_VERSION} && \
    ./configure \
          --prefix=${NGINX_HOME} \
          --with-http_ssl_module \
          --with-http_gzip_static_module \
          --conf-path=/etc/nginx/nginx.conf \
          --http-log-path=/var/log/nginx/access.log \
          --error-log-path=/var/log/nginx/error.log \
          --sbin-path=/usr/sbin/nginx \
          --pid-path=/var/run/nginx.pid && \
    make && \
    make install && \
    mkdir -p /etc/nginx/conf.d && \
    apk del curl gnupg build-base && \
    apk add git && \
    rm /nginx-${NGINX_VERSION}.tar.gz /nginx-${NGINX_VERSION}.tar.gz.asc && \
    rm -rf \
    /usr/share/man \
    /var/cache/apk/* \
    /nginx-${NGINX_VERSION} 

EXPOSE 80 443
CMD ["nginx", "-g", "daemon off;"]