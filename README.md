# 开始



## builder

提交构建基本编译环境的构建脚本。



## chromium-builder

在 **builder** 的基础上，添加 **java** 和 **depot_tools**，使其满足 chromium 的编译，也适用于编译 Android 系统。

> **温馨提示：**
>
> 由于 jdk 体积较大，在这里并没有上传，因此构建 chromium-builder 环境时，需要使用者自行下载 jdk。如果 jdk 的名称不是 jdk-8u231-linux-x64.tar.gz，还需要修改 Docker 脚本：
>
> ADD jdk-8u231-linux-x64.tar.gz /opt
> ENV JAVA_HOME /opt/jdk1.8.0_231



## 使用

1. 没有容器时，运行一个可交互的容器

  ```shell
  docker run -h iptv_builder --name iptv_builder -it chromium-builder /bin/bash
  ```

  >-h 主机名称（默认是随机字符串，可自定义），可选
  >
  >--name 容器名称

2. 有容器时，以可交互方式启动容器（也可以使用 1 运行一个新的容器）

  由于容器 iptv_builder 在 start 后会立刻退出，所以加上 -i 才能进行交互

  ```shell
  docker start -i iptv_builder
  ```

3. 如果容器运行了，进入容器的方式

  ```shell
  docker exec -it iptv_builder /bin/bash
  ```



> **扩展知识：**
>
> docker 规定容器内 pid 为 1 的进程退出，整个容器就会退出。例如：
>
> 1. docker start -i iptv_builder
>
>    这个命令是启动名称为 iptv_builder 的容器，-i 为交互式
>
> 2. docker exec -it iptv_builder /bin/bash
>
>    在执行这个命令，也能进入 iptv_builder。但是，如果 1 退出（也就是 pid 为 1 的进程退出），那么这个命令也跟随结束。
>
> 这也就能解释，为什么 docker start iptv_builder（没有 -i 参数）启动后接着就退出了。因为 docker start iptv_builder 运行 pid 为 1 的进程不需要与用户交互，很快就结束了。
>
> 而 -i 参数恰好运行了 /bin/bash (其 pid 为 1）与用户交互，只要交互没有结束，容器就会一直运行着。