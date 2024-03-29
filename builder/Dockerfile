FROM ubuntu:18.04
MAINTAINER Eniso <eniso-92@qq.com>

ARG GIT_USER_NAME=Eniso
ARG GIT_USER_EMAIL=eniso-92@qq.com

# 去除所有本地化的设置
RUN sh -c '/bin/echo -e "\nexport LC_ALL=C" >> ~/.bashrc'

# 更换源
RUN apt-get clean && apt-get autoremove -y && rm -rf /var/lib/{apt,dpkg,cache,log} /tmp/* /var/tmp/* && \
    perl -pi -e 's/archive.ubuntu.com/mirrors.aliyun.com/' /etc/apt/sources.list && \
    perl -pi -e 's/security.ubuntu.com/mirrors.aliyun.com/' /etc/apt/sources.list && \
    echo "Acquire::Retries \"5\";" > /etc/apt/apt.conf.d/70debconf

# 安装基础工具（支持 Android 编译 https://source.android.com/setup/build/initializing.html）
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update -y && \
    apt-get install -y --fix-missing \
        sudo lsb-base lsb-release apt-utils bash-completion busybox vim pigz python gcc-4.8 g++-4.8 \
        git git-core subversion gnupg flex bison gperf build-essential m4 ccache zip curl wget \
        zlib1g-dev gcc-multilib g++-multilib libc6-dev \
        lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev libgl1-mesa-dev libxml2-utils xsltproc \
        bc u-boot-tools gawk tofrodos python-markdown python-networkx libnss-sss

# 配置 gcc 和 g++
RUN rm /usr/bin/gcc /usr/bin/g++; ln -s /usr/bin/gcc-4.8 /usr/bin/gcc; ln -s /usr/bin/g++-4.8 /usr/bin/g++

# 配置 git
RUN git config --global user.mame "${GIT_USER_NAME}" && git config --global user.email "${GIT_USER_EMAIL}"

# 自动补全
RUN sh -c '/bin/echo -e "\n. /usr/share/bash-completion/bash_completion" >> ~/.bashrc'

# 配置时区、静默安装等
RUN echo Asia/Shanghai > /etc/timezone && \
    echo tzdata tzdata/Areas select Asia | debconf-set-selections && \
    echo tzdata tzdata/Zones/Asia select Shanghai | debconf-set-selections && \
    echo ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true | debconf-set-selections

# 安装编译工具（支持 Chromium 编译）
COPY install-build-deps.sh /tmp
COPY install-build-deps-android.sh /tmp
RUN chmod +x /tmp/install-build-deps.sh && \
    chmod +x /tmp/install-build-deps-android.sh && \
    /tmp/install-build-deps-android.sh

RUN apt-get clean && apt-get autoremove -y && rm -rf /var/lib/{apt,dpkg,cache,log} /tmp/* /var/tmp/*

# 替换 make 为 3.81 版本（Android 4.4.2 等系统会校验 make 的版本 3.81 或 3.82，而 3.81 比较保险）
COPY make /usr/bin/make
# 添加 repo
COPY repo /usr/bin/repo

# 工作目录
WORKDIR /home

# 启动一个文件浏览器（用户名/密码：admin/admin），方便文件传输
COPY filebrowser /usr/local/bin
RUN chmod +x /usr/local/bin/filebrowser
CMD ["/usr/local/bin/filebrowser", "-a", "0.0.0.0", "-r", "/home"]
