# The default ("latest") tag for the jalpine image is the Server JRE
FROM jonjack/jalpine

# Play requires bash for its start script
RUN echo 'http://dl-4.alpinelinux.org/alpine/v3.3/main' >> /etc/apk/repositories && \
    apk upgrade --update && \
    apk add bash

# expose Netty's default port
EXPOSE 9000

# You may need to customize the PID path if working on Mac OSX because 
# the default PID path is the application home and there are currently 
# permission issues if mounting the application files from the host
# ie. if mounting the application files from the host
# -v /host/app/play:/app/play then /app/play will be the default path for
# Play to attempt to write the PID file, but this currently fails because the
# process will not have the correct permissions on the mounted host directory
# CMD ["/app/play/bin/play-start-script", "-Dpidfile.path=/var/run/play.pid"]

CMD ["/app/play/bin/start"]