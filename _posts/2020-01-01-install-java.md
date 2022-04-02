---
layout: post
title: 在Linux上安装JDK
categories: java
description: 在Linux上安装JDK
keywords: java
---

介绍如何在Linux上安装JDK，若Linux上已经安装了JDK，则不需要重复安装；若没有安装，可参考该指导进行安装。以下以 **jdk-8u144-linux-x64.tar.gz** 为例介绍安装方法。

1. 源码包准备：通过官网下载 [JDK。](https://www.oracle.com/java/technologies/downloads/)

2. 解压源码包
   a. 通过终端在“/usr/local/”目录下新建文件夹**“java”**。
    ```
    sudo mkdir /usr/local/java
    ```
    b. 将下载的压缩包拷贝到“java”文件夹中。
    ```
    cp jdk-8u144-linux-x64.tar.gz /usr/local/java
    ```
    c. 进入“java”文件夹。
    ```
    cd /usr/local/java

    ```
    d. 解压压缩包。
    ```
    sudo tar -xvf jdk-8u144-linux-x64.tar.gz

    ```
    e. 删除压缩包。
    ```
    sudo rm jdk-8u144-linux-x64.tar.gz

    ```
3. 设置JDK环境变量
采用的全局设置方法，即修改“/etc/profile”，它是所有用户共用的环境变量。
    a. 打开文件“/etc/profile”。

    ```
    sudo vim /etc/profile
    ```

    b. 在文件末尾添加以下代码段。

    ```
    export JAVA_HOME=/usr/local/java/jdk1.8.0_144
    export JRE_HOME=/usr/local/java/jdk1.8.0_144/jre
    export CLASSPATH=.:$JAVA_HOME/LIB/DT.JAR:$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib:$CLASSPATH
    export PATH=$JAVA_HOME/bin:$PATH
    ```

    > 说明：
在添加上述代码过程中，请注意：
不要在等号（“=”）前后添加空格。
每个变量之间用冒号（“:”）隔开，而非分号（“;”）。

    c. 保存修改。
    ```
    source /etc/profile
    ```
4. 检验是否安装成功
    ```
    java -version
    ```
    显示以下内容时，表示安装成功。

```
java version "1.8.0_144" Java(TM) SE Runtime Environment (build 1.8.0_144-b03) Java HotSpot(TM) 64-Bit Server VM (build 25.77-b03, mixed mode)
```