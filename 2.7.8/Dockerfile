# Docker image contains:
# - CentOS 7
# - basic Linux functions (curl, wget, python, etc)
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

ENV CATALINA_BASE /tomcat
ENV SESAME_VERSION 2.7.8
ENV SESAME_DATA /data
ENV JAVA_MAXMEMORY 4096


# -----------------------------------------------------------------------------
# Import the Centos-7 RPM GPG key to prevent warnings and Add EPEL Repository
# -----------------------------------------------------------------------------
RUN rpm --import http://mirror.centos.org/centos/RPM-GPG-KEY-CentOS-7 \
	&& rpm --import http://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7 \
	&& rpm -Uvh http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-5.noarch.rpm

# Install updates
RUN yum -y update && yum clean all