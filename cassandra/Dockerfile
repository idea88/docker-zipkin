# Share the same base image to reduce layers used in testing
FROM openzipkin/jre-full:1.8.0_72
MAINTAINER OpenZipkin "http://zipkin.io/"

ENV ZIPKIN_VERSION 1.5.1

# Temporarily hard-code zipkin's configuration to a class that looks up the container's IP
ADD ZipkinConfigurationLoader.class /cassandra/build/classes/main/ZipkinConfigurationLoader.class
ENV CASSANDRA_VERSION=3.0.8 \
    JAVA=/usr/local/java/jre/bin/java \
    JVM_OPTS="-Dcassandra -Dcassandra.config.loader=ZipkinConfigurationLoader -Djava.net.preferIPv4Stack=true"

# Add patch files needed to work around python incompatibility
COPY CASSANDRA-11850/ /cassandra/CASSANDRA-11850

ADD install.sh /usr/local/bin/install
RUN /usr/local/bin/install

ADD run.sh /usr/local/bin/run.sh
CMD /usr/local/bin/run.sh

EXPOSE 9160 7000 7001 9042 7199
