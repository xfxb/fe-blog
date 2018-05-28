# fe-blog
幸福西饼前端团队技术博客。[访问地址][1]

## 使用说明

### 初次使用

保证已经安装nodejs 和 git。

进入项目更目录，按一下步骤操作：

1. 安装 hexo-cli：`npm install -g hexo-cli`
2. 安装依赖包：`npm install`
3. 启动本地服务，在本地预览：`hexo server`

### 写文章

1. 创建文件：`hexo new <file name>`。如果文件名有空格，请使用引号引起来。生成的文件放在`source/posts` 目录下。

生成的文件模板的头部信息如下：

```yaml
---
title: test demo # 文章标题， 默认是文件名字，你可以改变
date: 2018-05-14 14:12:15 # 文章生成日期，就用默认的
author: 杨永鹏 # 作者姓名
email: # 你邮箱
categories: # 分类 不填
- js # 标签 必填
tags:
- es5
- Decorator
---
# 开始文章正文
```

如果一篇文章短时间写不完，可以先以草稿的信息先保存，不发表，等完成后，才发表。

生成草稿：`hexo new draft <file name>`

发表草稿： `hexo publish <draft file name>`

本地服务预览草稿文件：`hexo server --draft`

### 把文章部署到服务器

1. 生成静态文件：`hexo g`。 `hexo g` 是 `hexo generate`简写。
2. 讲生成的静态文件部署到服务器上：`hexo deploy`。

    也可以将以上2步合成一步：`hexo g -d` 或者 `hexo d -g`。

    还可以监控文件变动实时生成静态文件：`hexo generate --watch`。

### 把文章推送到远程代码库

    将源码保存到git仓库，操作和git一样。

### FQA

- `hexo` 命令失效。
    1. `_config.yml` 配置文件格式有误，经常丢失冒号后的空格。
    2. `package.json`里`hexo`字段不能删除，它用来标识这是一个hexo目录。

## 技术池

- js

- css

- html

- canvas

- svg

- webpack

- react

- vue

- nodejs

- weixin-app

- performance-optimization

- algorithm

- shell



## 参考

[hexo官网][2]


[1]:https://xfxb.github.io/fe-blog/ "博客GitHub访问地址"
[2]:https://hexo.io/ "hexo官网"
[3]:https://www.staticgen.com/ "A List of Static Site Generators for JAMstack Sites"