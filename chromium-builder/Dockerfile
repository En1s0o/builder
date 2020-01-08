FROM builder:latest
MAINTAINER Eniso <eniso-92@qq.com>

# 工作目录
WORKDIR /home

# 安装 Java
ADD jdk-8u231-linux-x64.tar.gz /opt
ENV JAVA_HOME /opt/jdk1.8.0_231
ENV JRE_HOME $JAVA_HOME/jre
ENV PATH $JAVA_HOME/bin:$PATH

# 安装 depot_tools
ADD depot_tools.tar.gz /opt
ENV PATH /opt/depot_tools:$PATH

CMD ["/bin/bash"]
