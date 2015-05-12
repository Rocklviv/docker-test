FROM ubuntu:14.04

MAINTAINER dchekirda@gmail.com
ENV TOMCAT_MAJOR_VERSION 7
ENV TOMCAT_MINOR_VERSION 7.0.55
ENV CATALINA_HOME /tomcat

RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections

RUN apt-get update && \
    apt-get install -yq --no-install-recommends wget pwgen ca-certificates && \
    apt-get install -y python-software-properties software-properties-common && \
    add-apt-repository ppa:webupd8team/java &&\
    apt-get update &&\
    apt-get install -y oracle-java7-installer &&\
    apt-get install -y oracle-java7-set-default

# INSTALL TOMCAT
RUN wget -q https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz && \
    wget -qO- https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz.md5 | md5sum -c - && \
    tar zxf apache-tomcat-*.tar.gz && \
    rm apache-tomcat-*.tar.gz && \
    mv apache-tomcat* tomcat

RUN apt-get install -y supervisor &&\
    mkdir -p /var/log/supervisor &&\
    mkdir -p /etc/supervisor/conf.d

# Adding supervisor configuration.
ADD supervisor.conf /etc/supervisor.conf
# Adding tomcat configuration to supervisor.
ADD tomcat.conf /etc/supervisor/conf.d/tomcat.conf
# Adding bash file to create a admin user for tomcat.
ADD create_tomcat_admin_user.sh /tomcat/create_tomcat_admin_user.sh
# Adding run script
ADD run.sh /tomcat/run.sh
RUN chmod +x /tomcat/*.sh

# Creating admin user.
#CMD ["/tomcat/create_tomcat_admin_user.sh"]
ENTRYPOINT /tomcat/run.sh
