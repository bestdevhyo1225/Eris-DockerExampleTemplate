FROM ubuntu:latest
MAINTAINER kukaro <justkukaro@naver.com>
RUN apt-get update
RUN apt-get install -y openssh-server
RUN mkdir /var/run/sshd

#Set argument
ENV HOME_DIR /root

#set password
RUN echo 'root:root' |chpasswd

#replace sshd_config
RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

#make .ssh
RUN mkdir /root/.ssh

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

#Install nginx
RUN apt-get update && apt-get install -y vim
RUN apt-get update && apt-get install -y nodejs
RUN apt-get update && apt-get install -y npm
RUN npm install -g pm2

#Add file
ADD ./run ${HOME_DIR}/run
ADD ./was ${HOME_DIR}/was

RUN cd ${HOME_DIR}/was && npm install

EXPOSE 22 80

CMD ["/usr/sbin/sshd", "-D"]
