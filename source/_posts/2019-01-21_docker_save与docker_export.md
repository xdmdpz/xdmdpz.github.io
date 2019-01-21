---
title: docker_save与docker_export
date: 2019-01-21 13:40:40
tags: docker
header-img: "img/header_img/archive-bg.png"
subtitle: "记录思考"
---

再看docker 命令的时候发现了这几个方法


```shell
docker   # docker 命令帮助

Commands:
    
    export    Stream the contents of a container as a tar archive   
              # 导出容器的内容流作为一个 tar 归档文件[对应 import ]
    import    Create a new filesystem image from the contents of a tarball  
              # 从tar包中的内容创建一个新的文件系统映像[对应 export]
    load      Load an image from a tar archive              
    		  # 从一个 tar 包中加载一个镜像[对应 save]
    save      Save an image to a tar archive                
    	      # 保存一个镜像为一个 tar 包[对应 load]
```



下面是区别：

总结来说就是容器打包和镜像打包

- `docker save images_name`：将一个镜像导出为文件，再使用`docker load`命令将文件导入为一个镜像，会保存该镜像的的所有历史记录。比`docker export`命令导出的文件大，很好理解，因为会保存镜像的所有历史记录。
- `docker export container_id`：将一个容器导出为文件，再使用`docker import`命令将容器导入成为一个新的镜像，但是相比`docker save`命令，容器文件会丢失所有元数据和历史记录，仅保存容器当时的状态，相当于虚拟机快照。