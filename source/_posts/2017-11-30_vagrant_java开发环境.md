---
title: vagrant_java开发环境
date: 2017-11-30 20:11:33
tags: vagrant java
header-img: "img/header_img/archive-bg.png"
subtitle: "自用vagrant镜像"
---



- ubuntu 16.04
- jdk8
- tomcat8
- mysql5.7

maven啥的没弄进来，此版本只为了快速体验



快速体验 

1. 安装vagrant  [下载地址](https://www.vagrantup.com/downloads.html)

2. 安装virtual [下载地址](https://www.virtualbox.org/)

3. 把下载的 box加到box列表

   > `vagrant box add ubuntu_dev ~/Download/ubuntu_dev.box`
   >
   > ubuntu_dev 是镜像名称自定义
   >
   > 后面的是box路径 能找到就行

4. 建几个文件夹

   > `mkdir  /vagrant/vagrant_dev && cd /vagrant/vagrant_dev` 
   >
   > 配置存放目录
   >
   > `mkdir /vagrant/vagrant_dev/data`
   >
   > 文件共享目录
   >
   > `mkdir /vagrant/vagrant_dev/webapps`
   >
   > tomcat的webapps目录
   >
   > 纯粹个人喜好
   >
   > 开心就好

5. 把下载的 `Vagrantfile`  文件放进去

   > `cp ~/Download/Vagrantfile  /vagrant/vagrant_dev`
   >
   > 能复制进去就行
   >
   > 啥操作都行

6. 把配置文件里面的 `config.vm.box = "ubuntu_dev"` 改成你加到box列表的镜像名

7. 启动 

   > `vagrant up` 

8. 连接虚拟机

   > `vagrant ssh`
   >
   > 用户名 vagrant
   >
   > 密码 123
   >
   > 在`vagrant up`的log里面有22端口的映射
   >
   > 使用ssh工具连接
   >
   > 也可以配置内网ip使用22端口ssh

9. 虚拟机中命令

   1. mysql
      1. 启动 `sudo service mysql start`
      2. 关闭 `sudo service mysql stop`
   2. tomcat
      1. 启动`sudo service tomcat8 start`
      2. 关闭`sudo service tomcat8 shutdwon`