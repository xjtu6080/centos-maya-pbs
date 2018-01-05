#install pbspro on the mayabase
###build maya-centos
FROM maya-centos

MAINTAINER zxj

#ssh need dependent libraries
RUN yum install -y openssh-clients net-tools vim passwd openssl openssh-server

#pbspro need dependent libraries
RUN yum install -y rpm-build gcc autoconf automake libtool hwloc-devel libX11-devel libXt-devel libedit-devel libical-devel ncurses-devel postgresql-devel python-devel python-devel tcl-devel tk-devel swig expat-devel openssl-devel libXext libXft

#rpm-build the pbspro 
RUN mkdir -p /root/rpmbuild/SOURCES/
#ADD pbspro-14.1.0.tar.gz /root/rpmbuild/SOURCES/

#pbspro-14.1.0  download url https://github.com/PBSPro/pbspro/archive/v14.1.0.tar.gz

#RUN cd /root/rpmbuild/SOURCES/ && tar zcvf pbspro-14.1.0.tar.gz pbspro-14.1.0 
RUN cd /root/rpmbuild/SOURCES/ && \
	wget https://github.com/PBSPro/pbspro/archive/v14.1.0.tar.gz && \
	tar zxvf v14.1.0.tar.gz && mv v14.1.0.tar.gz pbspro-14.1.0.tar.gz
RUN cd /root/rpmbuild/SOURCES/pbspro-14.1.0 && rpmbuild -ba pbspro.spec 
RUN yum install -y  ssh-keygen -t rsa -P '' -f /root/.ssh/id_rsa  &&  cd /root/.ssh/ &&  cp id_rsa.pub  authorized_keys  &&  ssh-keygen -t rsa -P '' -f /etc/ssh/ssh_host_rsa_key  && ssh-keygen -t dsa -P '' -f /etc/ssh/ssh_host_dsa_key &&  ssh-keygen -t rsa -P '' -f /etc/ssh/ssh_host_ecdsa_key && ssh-keygen -t rsa -P '' -f /etc/ssh/ssh_host_ed25519_key && /usr/sbin/sshd
