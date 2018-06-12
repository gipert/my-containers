FROM gipert/centos-base:latest

USER root

RUN yum install -y -q lsyncd && \
    yum -q clean all

WORKDIR /data
CMD /usr/bin/lsyncd
