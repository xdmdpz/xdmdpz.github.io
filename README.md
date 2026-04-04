# IF Blog

基于 Hexo 的个人博客，使用 beantech 主题。

## 素材目录

`整理前的素材/` - 博客文章素材，整理后移到 `source/_posts/`

## 快速开始

```bash
npm install
hexo server      # 本地预览 http://localhost:4000
hexo clean && hexo generate && hexo deploy  # 发布
```

## 部署结构

- `hexo` 分支：博客源码
- `master` 分支：生成的静态文件（由 hexo-deployer-git 自动推送）

## 文章写作

```bash
hexo new "文章标题"   # 创建新文章
```

文章放在 `source/_posts/` 目录下。

## 配置

主要配置文件：`_config.yml`  
主题配置：`themes/beantech/_config.yml`
