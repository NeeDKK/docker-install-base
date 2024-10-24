FROM docker.needkk.com/centos:7

# Update CentOS base repository to use Aliyun mirrors
RUN sed -i.bak \
        -e 's|^mirrorlist=.*|#mirrorlist=|g' \
        -e 's|^#baseurl=http://mirror.centos.org|baseurl=https://mirrors.aliyun.com|g' \
        /etc/yum.repos.d/CentOS-Base.repo

RUN yum install -y \
    gcc \
    make \
    wget \
    vim \
    net-tools \
    bind-utils \
    git \
    tree \
    && yum clean all

RUN git clone https://github.com/z3APA3A/3proxy.git /usr/local/src/3proxy

WORKDIR /usr/local/src/3proxy
RUN make -f Makefile.Linux

RUN mkdir -p /usr/local/3proxy/bin \
    && cp /usr/local/src/3proxy/bin/3proxy /usr/local/3proxy/bin/3proxy

RUN mkdir -p /etc/3proxy

EXPOSE 3128

# 设置启动命令
CMD ["/usr/local/3proxy/bin/3proxy", "/etc/3proxy/3proxy.cfg"]

# 清理不必要的文件
RUN rm -rf /usr/local/src/3proxy