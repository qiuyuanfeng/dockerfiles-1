FROM ubuntu
MAINTAINER bjozsa@att.com

ENV container docker
RUN apt-get -y update

RUN apt-get update -qq && apt-get install -qqy \
    apt-transport-https \
    ca-certificates \
    curl \
    lxc \
    vim \
    iptables

RUN curl -sSL https://get.docker.com/ | sh

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;

COPY scripts/kubeadm.sh /usr/local/bin/kubeadm.sh
RUN chmod +x /usr/local/bin/kubeadm.sh

VOLUME /sys/fs/cgroup
VOLUME /var/run/docker.sock

CMD /sbin/init
