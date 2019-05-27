---
layout:   post
title:    "Java 启程之路"
subtitle: "Start with Java: 在 Ubuntu/Mint 上安装 Oracle Java"
date:     2019-05-27
author:   "Eric"
catalog:  true
header-img: "img/in-post/post-start-with-java/home-bg-o.jpg"
tags:
  - Linux
  - Ubuntu
  - Linux Mint
  - Java
---

## 1 去官网，选择下载一个 Oracle Java 二进制文件
该二进制文件以 `tar.gz` 结尾

![download-java][1]

## 2 解压 Oracle Java 二进制文件
在目录 `/usr/local/java`（如没有，可自行新建） 中，解压
```sh
cd ~/Downloads/
sudo cp -r jdk-8u161-linux-x64.tar.gz /usr/local/java
cd /usr/local/java
sudo tar xzf jdk-8u161-linux-x64.tar.gz
sudo mv jdk1.8.0_161/ jdk1.8　　　　　　　# 改名，便于后续操作
```

![unzip-java][2]

## 3 更改系统 PATH 
### 3.1 打开系统的全局配置文件
```sh
vi /etc/profile
```

### 3.2 在文件末尾，添加以下内容，保存文件并退出
```sh
JAVA_HOME=/usr/local/java/jdk1.8
PATH=$PATH:$JAVA_HOME/bin
JRE_HOME=/usr/local/java/jdk1.8/jre
PATH=$PATH:$JRE_HOME/bin
export JAVA_HOME
export JRE_HOME
export PATH
```

## 4 通知系统关于更新后的 Oracle Java 版本信息
### 4.1 通知 Ubuntu Linux 系统 Oracle Java JRE/JDK 的所在位置
```sh
sudo update-alternatives --install "/usr/bin/java" "java" "/usr/local/java/jdk1.8/jre/bin/java" 1
sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/local/java/jdk1.8/bin/javac" 1
sudo update-alternatives --install "/usr/bin/javaws" "javaws" "/usr/local/java/jdk1.8/jre/bin/javaws" 1
```

![update-alternative-java][3]

### 4.2 把 Oracle Java JRE 1.8 设定为新的默认 Java 应用
```sh
sudo update-alternatives --set java /usr/local/java/jdk1.8/jre/bin/java
sudo update-alternatives --set javac /usr/local/java/jdk1.8/bin/javac
sudo update-alternatives --set javaws /usr/local/java/jdk1.8/jre/bin/javaws
```

![set-default-java][4]


### 4.3 输入以下命令重载 /etc/profile 文件内的系统范围内的 PATH
```sh
. /etc/profile 
```

注意，`/etc/profile` 文件中的系统范围内的 `PATH` 将在重启 `Ubuntu` 系统后被重载

## 5 查看 Java 版本
```sh
java -version
```

![java-version][5]

[1]: /img/in-post/post-start-with-java/download-java.png
[2]: /img/in-post/post-start-with-java/unzip-java.png
[3]: /img/in-post/post-start-with-java/update-alternative-java.png
[4]: /img/in-post/post-start-with-java/set-default-java.png
[5]: /img/in-post/post-start-with-java/java-version.png