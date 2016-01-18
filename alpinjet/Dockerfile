FROM jonjack/jalpine

ENV JETTY_VERSION 9.3.5.v20151012
ENV JETTY_HOME=/opt/jetty-distribution-${JETTY_VERSION}
ENV PATH $PATH:$JETTY_HOME/bin

RUN curl -s https://repo1.maven.org/maven2/org/eclipse/jetty/jetty-distribution/${JETTY_VERSION}/jetty-distribution-${JETTY_VERSION}.tar.gz | tar -xzf - -C /opt

RUN printf 'cd $JETTY_HOME/demo-base\njava -jar $JETTY_HOME/start.jar' > /root/demo-jetty.sh &&\
    chmod 555 /root/demo-jetty.sh

EXPOSE 8080
CMD /root/demo-jetty.sh