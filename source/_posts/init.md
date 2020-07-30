---
title: 博客初始化
top: true
cover: false
toc: true
mathjax: true
date: 2020-07-28 09:11:29
password:
summary: 博客初始化
tags:
- blog写作
- blog发布
categories:
- blog相关
---

## 安装Node.js
安装稳定版，否则不支持hexo deploy。

**添加镜像源**：`npm config set registry https://registry.npm.taobao.org`

## 安装hexo
`npm i hexo-cli -g`

`npm i hexo-deployer-git` \#发布扩展

## Hexo常用命令
npm install hexo -g \#安装Hexo
npm update hexo -g \#升级
hexo init \#初始化博客

命令简写
hexo n "我的博客" == hexo new "我的博客" \#新建文章
hexo g == hexo generate \#生成
hexo s == hexo server \#启动服务预览
hexo d == hexo deploy \#部署

hexo server \#Hexo会监视文件变动并自动更新，无须重启服务器
hexo server -s \#静态模式
hexo server -p 5000 \#更改端口
hexo server -i 192.168.1.1 \#自定义 IP
hexo clean \#清除缓存，若是网页正常情况下可以忽略这条命令

## 配置文件
在blog根目录里的_config.yml文件称为**站点**配置文件。根目录里的themes文件夹，里面也有个_config.yml文件，这个称为**主题**配置文件

## 评论

### gitalk
在主题的_config.yml文件中，设置gitalk的Client ID、Client Secret。由Github的OAuth Application提供，[链接](https://github.com/settings/applications/new)

### valine
详情见[Valine](https://valine.js.org/)

## 文件开头
title: 文章标题
catalog: 是否显示段落目录
date: 文章日期
subtitle: 子标题
header-img: 顶部背景图片
top: 是否置顶
tags: 标签
categories: 分类
