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
RUN ln -s /opt/${JDK_VERSION} /opt/jdk && sh -c '/bin/echo -e "\nexport JAVA_HOME=/opt/jdk\nexport JRE_HOME=\$JAVA_HOME/jre\nexport PATH=\$JAVA_HOME/bin:\$PATH" >> ~/.bashrc'

# 安装 depot_tools，禁止 depot_tools 自动更新
# git clone https://chromium.googlesource.com/chromium/tools/depot_tools
# 最新   master
# 2018/1 dbc809fcd3be3d9a39b77af038bbcdcc3db25e2f
# 2017/3 0bbe6fa00ef873080c4f6d145ea7a00497eeed3f
# 2016/2 dbb6f8246b47bbf47848618d7ae089f9233d0171
ADD depot_tools.tar.gz /opt
RUN cd /opt/depot_tools && \
    git checkout 0bbe6fa00ef873080c4f6d145ea7a00497eeed3f && \
    sh -c '/bin/echo -e "\nexport DEPOT_TOOLS_UPDATE=0\nexport PATH=/opt/depot_tools:\$PATH" >> ~/.bashrc'

# 如果需要用到 gcc-linaro 编译链（例如：Amlogic Android 系统源码用到）
# 一定要注意 gcc-linaro 的版本，下面是本人测试成功的版本
# https://releases.linaro.org/archive/14.09/components/toolchain/binaries/gcc-linaro-aarch64-linux-gnu-4.9-2014.09_linux.tar.xz
ADD gcc-linaro-aarch64-linux-gnu-4.9-2014.09_linux.tar.xz /opt
RUN sh -c '/bin/echo -e "\nexport PATH=/opt/gcc-linaro-aarch64-linux-gnu-4.9-2014.09_linux/bin:\$PATH" >> ~/.bashrc'

# 如果需要用到特定的编译链，可以自行添加，例如：
# 1. 海思 MV100 编译链，一般都内置在工程代码里面了，根据说明文档配置即可
# 2. 海思 MV300 编译链，在 source 之后就会自动配置好了

# 工作目录
WORKDIR /home

