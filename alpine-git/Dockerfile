FROM alpine

RUN echo 'http://dl-4.alpinelinux.org/alpine/v3.3/main' >> /etc/apk/repositories && \
  apk upgrade --update && \
  apk add git