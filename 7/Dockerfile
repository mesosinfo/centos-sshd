# DOCKER-VERSION 1.12
# VERSION        0.1
# SOURCE         https://github.com/mesosinfo/centos-sshd
FROM mesosinfo/centos-systemd:7.3
MAINTAINER Yong Zhang<zhangyong.net@gmail.com>
########################################################################## ### update glibc-common for locale files
RUN yum update -y glibc-common

##########################################################################
# all yum installations here
RUN yum install -y net-tools
RUN yum install -y initscripts
RUN yum install -y sudo passwd openssh openssh-server openssh-clients
RUN yum install -y tar screen crontabs strace telnet perl libpcap bc patch ntp dnsmasq

##########################################################################
RUN ssh-keygen -f /etc/ssh/ssh_host_rsa_key -N '' -t rsa
RUN ssh-keygen -f /etc/ssh/ssh_host_ecdsa_key -N '' -t ecdsa

# start sshd to generate host keys, patch sshd_config and enable yum repos
RUN (service sshd start; \
     sed -i 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config; \
     sed -i 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config; \
     sed -i 's/#PermitRootLogin yes/PermitRootLogin yes/' /etc/ssh/sshd_config)

##########################################################################
# passwords 
RUN echo "root:rootroot" | chpasswd

#
#systemctl enable sshd.service
#systemctl start sshd.service

#
EXPOSE 22
#
CMD ["/usr/sbin/init"]
