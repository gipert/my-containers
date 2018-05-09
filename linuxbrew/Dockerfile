FROM centos:7

RUN yum -q -y update && \
    yum -q install -y zsh curl make ruby sudo which && \
    yum -q clean all

RUN localedef -i en_US -f UTF-8 en_US.UTF-8 \
	&& useradd -m -s /bin/bash linuxbrew \
	&& echo 'linuxbrew ALL=(ALL) NOPASSWD:ALL' >>/etc/sudoers

USER linuxbrew
WORKDIR /home/linuxbrew

ENV PATH=/home/linuxbrew/.linuxbrew/bin:/home/linuxbrew/.linuxbrew/sbin:$PATH \
	SHELL=/bin/bash \
	USER=linuxbrew

RUN yes | ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Linuxbrew/install/master/install)" \
	&& brew config

CMD /bin/zsh
