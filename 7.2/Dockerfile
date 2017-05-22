# DOCKER-VERSION 1.10.3
# VERSION        0.1
# SOURCE         https://github.com/mesosinfo/centos-sshd

FROM centos:7
MAINTAINER Yong Zhang<zhangyong.net@gmail.com>
########################################################################## ### update glibc-common for locale files
RUN yum update -y glibc-common

##########################################################################
# all yum installations here
RUN yum install -y sudo passwd openssh-server openssh-clients tar screen crontabs strace telnet perl libpcap bc patch ntp dnsmasq
#RUN yum install -y sudo passwd openssh-server openssh-clients tar screen crontabs strace telnet perl libpcap bc patch ntp

##########################################################################
# add epel repository
# RUN rpm -Uvh http://mirror.centos.org/centos/7/extras/x86_64/Packages/epel-release-7-9.noarch.rpm

# RUN (rpm -Uvh https://yum.puppetlabs.com/el/7/products/i386/puppetlabs-release-22.0-2.noarch.rpm; \
#     yum install -y puppet puppet-server puppetserver facter hiera)

# start sshd to generate host keys, patch sshd_config and enable yum repos
RUN (service sshd start; \
     sed -i 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config; \
     sed -i 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config; \
     sed -i 's/#PermitRootLogin yes/PermitRootLogin yes/' /etc/ssh/sshd_config; \
     sed -i 's/enabled=0/enabled=1/' /etc/yum.repos.d/CentOS-Base.repo)

RUN (mkdir -p /root/.ssh/; \
     echo "StrictHostKeyChecking=no" > /root/.ssh/config; \
     echo "UserKnownHostsFile=/dev/null" >> /root/.ssh/config)

##########################################################################
# passwords 
RUN echo "root:rootroot" | chpasswd

EXPOSE 22
CMD service crond start; /usr/sbin/sshd -D
