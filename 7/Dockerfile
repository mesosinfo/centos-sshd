# DOCKER-VERSION 1.10.3
# VERSION        0.1
# SOURCE         https://github.com/mesosinfo/centos-sshd

FROM centos:7
MAINTAINER Yong Zhang<zhangyong.net@qq.com>
########################################################################## ### update glibc-common for locale files
RUN yum -y install openssh openssh-clients openssh-server
EXPOSE 22
RUN ssh-keygen -f /etc/ssh/ssh_host_rsa_key -N '' -t rsa
RUN ssh-keygen -f /etc/ssh/ssh_host_ecdsa_key -N '' -t ecdsa
RUN echo "root:rootroot" | chpasswd
RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
CMD ["/usr/sbin/sshd", "-D"]
