---
title: CentOS-JAVA开发环境
date: 2018-10-11 11:11:33
tags: restful
header-img: "img/header_img/archive-bg.png"
subtitle: "最近在用vagrant做一个hadoop的集群，把安装java之类的命令提出来了"
---



### 安装jdk

- oracle jdk

```shell
yum -y remove java*

yum -y install wget
#具体版本替换下就好
wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u171-b11/512cd62ec5174c3487ac17c61aaa89e8/jdk-8u171-linux-x64.rpm
#具体版本替换
rpm -ivh jdk-8u171-linux-x64.rpm
```

- zulu openjdk

```
wget https://cdn.azul.com/zulu/bin/zulu8.33.0.1-jdk8.0.192-linux.x86_64.rpm
rpm -ivh zulu8.33.0.1-jdk8.0.192-linux.x86_64.rpm
```

- 环境变量配置

```
# 版本不同替换下
export JAVA_HOME=/usr/java/jdk1.8.0_171-amd64
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```



安装maven

```
wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo


yum -y install apache-maven
```

