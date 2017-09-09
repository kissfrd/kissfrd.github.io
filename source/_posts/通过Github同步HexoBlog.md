---
title: 通过 Github 同步 Hexo Blog
date: 2017-09-04 23:12:42
categories: Technique
tags:
- blog

---

## 思路

**Blog 内容**: 创建两个分支分别管理 blog 源文件和静态网页

* git push 推送博客源文件到 hexo 分支作为备份


* hexo d 推送静态网页到 master 分支更新 blog 页面

**Blog 主题**: 以 Submodule 方式管理主题 <!-- more -->

## 搭建流程

### Blog 内容

1.创建仓库: `username.github.io`

2.创建两个分支: master 与 hexo

3.设置 hexo 为默认分支

4.git clone 仓库到本地

5.在本地 `username.github.io` 目录下安装 hexo (当前分支为 hexo)

\* 安装过程中 `hexo init` 会删除 .git 文件夹; 要避免这一问题, 先把 hexo 安装到别的目录, 再拷贝过来即可.

6.修改 \_config.yml 文件中的 deploy 参数, 分支为 master

7.依次执行 `git add .` `git commit -m "..." ` `git push origin hexo` 提交 blog 源文件到 hexo 分支

8.执行 `hexo g -d` 生成网站并部署到 master 分支

### Blog 主题

1.在 Github 上 fork 自己喜欢的主题

2.在本地 `username.github.io` 目录下以 Submodule 方式添加已 fork 的主题:

```
git submodule add https://github.com/kissfrd/hexo-theme-next.git themes/next
```
3.主题配置发生改动后在其目录下 git push

## 多终端同步

### Blog 内容

1.git clone 仓库到本地

2.在本地 `username.github.io` 目录下安装 hexo (注: 本次安装不需要 `hexo init` 指令)

\* 只要把 hexo 和所需插件写入到 package.json 中 (安装时加 --save 参数会自动写入), 那么 git clone 下来之后,  `npm install` 就能装好 hexo 和所有的依赖

\* 另一台电脑 push, 部署后会改变之前博客的发布时间.

### Blog 主题

执行以下指令即可:

```
git submodule init
git submodule update
```



## 参考

- [使用 hexo, 如果换了电脑怎么更新博客? - 回答作者: CrazyMilk](https://zhihu.com/question/21193762/answer/79109280)
- [Using Git Submodules to Manage Your Custom Hexo Theme](http://jr0cket.co.uk/hexo/using-git-submodules-for-custom-hexo-theme.html)

