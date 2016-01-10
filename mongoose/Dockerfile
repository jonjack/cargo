FROM alpine

RUN echo 'http://dl-3.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories && \
    apk upgrade --update && \
    addgroup -S mongo && adduser -S -G mongo mongo && \
    apk add mongodb && \
    mkdir -p /app/mongo && chown mongo:mongo /app/mongo && \
    rm -rf /var/cache/apk/*

EXPOSE 27017
CMD ["mongod"]