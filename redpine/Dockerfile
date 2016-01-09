FROM alpine

RUN addgroup -S redis && adduser -S -G redis redis

# tar man
# --------------
# -f an archive file
# -x extract
# -v verbose
# -z filter the archive thru gzip (for .gz)

RUN echo 'http://dl-4.alpinelinux.org/alpine/v3.3/main' >> /etc/apk/repositories && \
    apk upgrade --update && \
    apk add redis && \
    rm -rf /var/cache/apk/*

RUN mkdir -p /app/redis && chown redis:redis /app/redis
VOLUME /app/redis
WORKDIR /app/redis

#COPY docker-entrypoint.sh /entrypoint.sh
#RUN chmod 777 /entrypoint.sh
#ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 6379 16379 26379
CMD [ "redis-server" ]