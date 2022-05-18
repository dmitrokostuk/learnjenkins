FROM centos

RUN rm -rf /run/nologin

RUN cd /etc/yum.repos.d/
RUN sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
RUN sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*

RUN yum -y install openssh-server openssh-clients

RUN useradd remote_user && \
    echo "remote_user:1234" | chpasswd\
    mkdir /home/remote_user/.ssh \
    chmod 700 /home/remote_user/.ssh

COPY remote-key.pub /home/remote_user/.ssh/authorized_keys

RUN chown remote_user:remote_user -R /home/remote_user/.ssh && \
    chmod 600 /home/remote_user/.ssh/authorized_keys

RUN ssh-keygen -A

RUN yum -y install mysql

RUN yum -y install gcc openssl-devel bzip2-devel libffi-devel zlib-devel xz-devel 

RUN yum -y install wget

RUN yum -y install make 


RUN wget https://www.python.org/ftp/python/3.7.11/Python-3.7.11.tgz  && \
    tar xzf Python-3.7.11.tgz  && \
    cd Python-3.7.11 && \
    ./configure --enable-optimizations && \
    make altinstall 

RUN python3.7 -V 

RUN set -xe \
    && yum update -y \
    && yum install -y python3-pip

RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    
    #python3.7 get-pip.py --user && \
    pip3 -V && \
    alias pip3='/root/.local/bin/pip3'&& \
    pip3 install awscli --upgrade --user




CMD /usr/sbin/sshd -D

EXPOSE 22



    

