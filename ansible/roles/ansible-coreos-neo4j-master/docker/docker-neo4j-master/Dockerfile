# DOCKER-VERSION 1.0.1
# VERSION        0.5
# mesos-master
FROM debian:jessie 
MAINTAINER Pablo Torres <pablo.torres.t@gmail.com>

RUN apt-get clean
RUN apt-get update -y
RUN apt-get install -y default-jre wget sed
RUN wget -O - http://debian.neo4j.org/neotechnology.gpg.key| apt-key add -
RUN echo 'deb http://debian.neo4j.org/repo stable/' > /etc/apt/sources.list.d/neo4j.list
RUN apt-get update
RUN apt-get install neo4j -y

ENV NEO4J_HOME /var/lib/neo4j
ENV $IPADDR `ip a s | sed -ne '/127.0.0.1/!{s/^[ \t]*inet[ \t]*\([0-9.]\+\)\/.*$/\1/p}'`
RUN echo $IPADDR
RUN sed -i "s|#org.neo4j.server.webserver.address=0.0.0.0|org.neo4j.server.webserver.address=$IPADDR|g" $NEO4J_HOME/conf/neo4j-server.properties
RUN sed -i "s|#node_auto_indexing|node_auto_indexing|g" $NEO4J_HOME/conf/neo4j.properties
RUN sed -i "s|#node_keys_indexable|node_keys_indexable|g" $NEO4J_HOME/conf/neo4j.properties

# http
EXPOSE 7474 

CMD /bin/bash -c 'ulimit -n 65536 ; .$NEO4J_HOME/bin/neo4j console'

