FROM alpine

RUN echo 'http://dl-4.alpinelinux.org/alpine/v3.3/main' >> /etc/apk/repositories && \
    apk upgrade --update && \
    addgroup -S redis && adduser -S -G redis redis && \
    apk add redis && \
    mkdir -p /app/redis && chown redis:redis /app/redis && \
    rm -rf /var/cache/apk/*

EXPOSE 6379 16379 26379
CMD [ "redis-server" ]