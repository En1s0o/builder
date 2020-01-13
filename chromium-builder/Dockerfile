FROM eniso/builder:latest
MAINTAINER Eniso <eniso-92@qq.com>

# 工作目录
WORKDIR /home

# 安装 Java
ADD jdk-8u231-linux-x64.tar.gz /opt
ENV JAVA_HOME /opt/jdk1.8.0_231
ENV JRE_HOME $JAVA_HOME/jre
ENV PATH $JAVA_HOME/bin:$PATH

# 安装 depot_tools，禁止 depot_tools 自动更新
# git clone https://chromium.googlesource.com/chromium/tools/depot_tools
# 最新   master
# 2018/1 dbc809fcd3be3d9a39b77af038bbcdcc3db25e2f
# 2017/3 0bbe6fa00ef873080c4f6d145ea7a00497eeed3f
# 2016/2 dbb6f8246b47bbf47848618d7ae089f9233d0171
ADD depot_tools.tar.gz /opt
RUN cd /opt/depot_tools && git checkout 0bbe6fa00ef873080c4f6d145ea7a00497eeed3f
ENV PATH /opt/depot_tools:$PATH
ENV DEPOT_TOOLS_UPDATE 0

CMD ["/bin/bash"]
