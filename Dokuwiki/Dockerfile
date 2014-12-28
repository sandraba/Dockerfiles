############################################################
# Dockerfile to build Dokuwiki container images
# Based on Centos
############################################################

FROM alfred/centos7

MAINTAINER Sandra Barteit "barteit@uni-heidelberg.de"

ENV DOKUWIKI_VERSION 2014-09-29b
ENV LANG en_US.UTF-8

#Install necessary software packages
RUN yum -y update
RUN yum -y install nginx php-gd php-fpm php-apc php-pecl-imagick php-mcrypt php-cgi wget tar openssh-server
RUN yum -y update


#Download and deploy Dokuwiki
RUN sudo wget -O /dokuwiki.tgz \
    "http://download.dokuwiki.org/src/dokuwiki/dokuwiki-$DOKUWIKI_VERSION.tgz"
RUN sudo tar -zxf dokuwiki.tgz
RUN sudo mv "/dokuwiki-$DOKUWIKI_VERSION" /usr/share/nginx/html/wiki

#Set up ownership
RUN sudo chown -R nginx:nginx /usr/share/nginx/html/wiki

#Cleanup
RUN sudo rm dokuwiki.tgz

#Configure PHP
RUN echo "cgi.fix_pathinfo=0;" >> /etc/php.ini

#Configure Nginx
COPY conf/wiki.conf /etc/nginx/conf.d/


EXPOSE 80
VOLUME ["/dokuwiki/data/","/dokuwiki/lib/plugins/","/dokuwiki/conf/","/dokuwiki/lib/tpl/","/var/log/"]

