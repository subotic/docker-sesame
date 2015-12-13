# Docker image contains:
# - CentOS 7
# - JRE 8
# - Tomcat 8
# - Sesame 2.7.8
#
# Credits go to:
# - https://github.com/jdeathe/centos-ssh
# - http://blog.zenika.com/index.php?post/2014/10/07/Setting-up-a-development-environment-using-Docker-and-Vagrant

FROM centos:7

MAINTAINER Ivan Subotic "ivan.subotic@unibas.ch"

ENV JAVA_VERSION 8u66

ENV TOMCAT_MAJOR_VERSION 8
ENV TOMCAT_MINOR_VERSION 8.0.30
ENV CATALINA_HOME /tomcat
ENV CATALINA_BASE /tomcat
ENV SESAME_VERSION 2.8.7
ENV SESAME_DATA /data
ENV JAVA_MAXMEMORY 4096

# -----------------------------------------------------------------------------
# IMPORT the Centos-7 RPM and EPEL Repository GPG key to prevent warnings
# -----------------------------------------------------------------------------
RUN rpm --import http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-7
# && rpm --import http://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7

#RUN yum -y install epel-release

# Base Install + JDK
RUN yum -y update && \
		yum -y install java-1.8.0-openjdk && \
		yum -y install java-1.8.0-openjdk-devel && \
		yum -y update bash && \
		rm -rf /var/cache/yum/* && \
		yum clean all

# Install Tomcat
RUN curl -sS -O https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz && \
    curl -sS https://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VERSION}/v${TOMCAT_MINOR_VERSION}/bin/apache-tomcat-${TOMCAT_MINOR_VERSION}.tar.gz.md5 | md5sum -c - && \
		tar zxf apache-tomcat-*.tar.gz && \
    rm apache-tomcat-*.tar.gz && \
    mv apache-tomcat* ${CATALINA_HOME}

# Remove docs and examples
RUN rm -rf $CATALINA_BASE/webapps/docs && \
		rm -rf $CATALINA_BASE/webapps/examples

# Install Sesame
RUN curl -sS -o /tmp/sesame.tar.gz -L http://sourceforge.net/projects/sesame/files/Sesame%202/$SESAME_VERSION/openrdf-sesame-$SESAME_VERSION-sdk.tar.gz/download && \
    tar -xzf /tmp/sesame.tar.gz -C /opt && \ 
		ln -s /opt/openrdf-sesame-$SESAME_VERSION /opt/sesame && \
		rm /tmp/sesame.tar.gz

# Deploy 
RUN mkdir ${CATALINA_BASE}/webapps/openrdf-sesame && \
		cd ${CATALINA_BASE}/webapps/openrdf-sesame && \
		jar xf /opt/sesame/war/openrdf-sesame.war && \
		mkdir ${CATALINA_BASE}/webapps/openrdf-workbench && \
		cd ${CATALINA_BASE}/webapps/openrdf-workbench && \
		jar xf /opt/sesame/war/openrdf-workbench.war


ADD run.sh /run.sh
RUN chmod +x /*.sh

EXPOSE 8080
CMD ["/run.sh"]