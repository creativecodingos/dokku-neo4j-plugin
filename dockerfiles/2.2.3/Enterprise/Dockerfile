FROM debian:wheezy
MAINTAINER Giacomo Triggiano "giacomo@creativecoding.it"

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        openjdk-7-jre \
        wget

ENV NEO4J_VERSION 2.2.3
ENV NEO4J_EDITION enterprise

RUN wget -O /var/neo4j.tar.gz "http://dist.neo4j.org/neo4j-$NEO4J_EDITION-$NEO4J_VERSION-unix.tar.gz" && \
    tar -xvzf /var/neo4j.tar.gz -C /var && \
    rm /var/neo4j.tar.gz && \
    mv "/var/neo4j-$NEO4J_EDITION-$NEO4J_VERSION" /var/neo4j

RUN sed -i 's@#org.neo4j.server.webserver.address=0.0.0.0@org.neo4j.server.webserver.address=0.0.0.0@' /var/neo4j/conf/neo4j-server.properties && \
    sed -i 's@dbms.security.auth_enabled=true@dbms.security.auth_enabled=false@' /var/neo4j/conf/neo4j-server.properties && \
    sed -i 's@org.neo4j.server.webserver.https.enabled=true@org.neo4j.server.webserver.https.enabled=false@' /var/neo4j/conf/neo4j-server.properties && \
    sed -i 's@#remote_shell_enabled=true@remote_shell_enabled=true@' /var/neo4j/conf/neo4j.properties && \
    sed -i 's@#remote_shell_host=127.0.0.1@remote_shell_host=0.0.0.0@' /var/neo4j/conf/neo4j.properties && \
    sed -i 's@#allow_store_upgrade=true@allow_store_upgrade=true@' /var/neo4j/conf/neo4j.properties && \
    sed -i 's@online_backup_server=127.0.0.1:6362@online_backup_server=0.0.0.0:6362@' /var/neo4j/conf/neo4j.properties

EXPOSE 7474

ADD ./bin/. /bin

RUN chmod +x /bin/start_neo4j.sh

CMD ["/bin/start_neo4j.sh"]
