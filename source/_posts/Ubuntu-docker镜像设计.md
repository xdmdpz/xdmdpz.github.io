在 Debian 或者 Ubuntu 或者它们的衍生版本中会用到 apt 包管理器，如果需要在镜像中安装新包，推荐的写法是

```
RUN apt-get update \
 && apt-get install -y \
      ${abc} \
      ${bcd} \
 && rm -rf /var/lib/apt/lists/*
```

几个要点：

1. 要用 apt-get，不要用 aptitude 和 apt 命令，这2个命令是给人机交互的，不是给脚本用的；
2. ${abc} ${bcd} 指按照字母顺序每行一个包排列；
3. rm 一行清理索引和缓存；
4. 以上几条命令要写在同一个 RUN 里，不然生成多个层起不到压缩镜像大小的作用。

