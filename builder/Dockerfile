FROM ubuntu:18.04
MAINTAINER Eniso <eniso-92@qq.com>

# 配置静默安装
RUN echo Asia/Shanghai > /etc/timezone && \
    echo tzdata tzdata/Areas select Asia | debconf-set-selections && \
    echo tzdata tzdata/Zones/Asia select Shanghai | debconf-set-selections && \
    echo ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true | debconf-set-selections

# 更换源
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak && \
    apt-get clean && apt-get autoremove -y && rm -rf /var/lib/{apt,dpkg,cache,log} /tmp/* /var/tmp/* && \
    perl -pi -e 's/archive.ubuntu.com/mirrors.aliyun.com/' /etc/apt/sources.list && \
    perl -pi -e 's/security.ubuntu.com/mirrors.aliyun.com/' /etc/apt/sources.list

# 安装基础工具
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y && \
    apt-get install -y --fix-missing \
        sudo \
        lsb-base \
        lsb-release \
        apt-utils \
        vim \
        busybox \
        curl \
        wget \
        git \
        subversion \
        python \
        build-essential

# 安装编译工具
ADD install-build-deps.sh /tmp
ADD install-build-deps-android.sh /tmp
RUN chmod +x /tmp/install-build-deps.sh && \
    chmod +x /tmp/install-build-deps-android.sh && \
    /tmp/install-build-deps-android.sh

RUN apt-get clean && apt-get autoremove -y && rm -rf /var/lib/{apt,dpkg,cache,log} /tmp/* /var/tmp/*

CMD ["/bin/bash"]
