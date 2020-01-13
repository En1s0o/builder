FROM eniso/builder:latest
MAINTAINER Eniso <eniso-92@qq.com>

ARG JDK_VERSION=jdk1.6.0_45
#ARG JDK_VERSION=jdk1.7.0_80
#ARG JDK_VERSION=jdk1.8.0_231

# 安装 Java
# JDK 6
WORKDIR /opt
COPY jdk-6u45-linux-x64.bin /opt
RUN /opt/jdk-6u45-linux-x64.bin && rm -f /opt/jdk-6u45-linux-x64.bin
# JDK 7
ADD jdk-7u80-linux-x64.tar.gz /opt
# JDK 8
ADD jdk-8u231-linux-x64.tar.gz /opt
# 配置 JDK
RUN ln -s /opt/${JDK_VERSION} /opt/jdk && echo -e "\r\nexport JAVA_HOME=/opt/jdk\r\nexport JRE_HOME=$JAVA_HOME/jre\r\nexport PATH=$JAVA_HOME/bin:$PATH\r\n" > /etc/profile

# 安装 depot_tools，禁止 depot_tools 自动更新
# git clone https://chromium.googlesource.com/chromium/tools/depot_tools
# 最新   master
# 2018/1 dbc809fcd3be3d9a39b77af038bbcdcc3db25e2f
# 2017/3 0bbe6fa00ef873080c4f6d145ea7a00497eeed3f
# 2016/2 dbb6f8246b47bbf47848618d7ae089f9233d0171

# 安装 repo

# 安装 depot_tools
ADD depot_tools.tar.gz /opt
RUN cd /opt/depot_tools && \
    git checkout 0bbe6fa00ef873080c4f6d145ea7a00497eeed3f && \
    echo -e "\r\nexport DEPOT_TOOLS_UPDATE=0\r\nexport PATH=/opt/depot_tools:$PATH\r\n" > /etc/profile

# 工作目录
WORKDIR /home

CMD ["/bin/bash"]
