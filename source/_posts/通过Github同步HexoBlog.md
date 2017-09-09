---
title: 通过 Github 同步 Hexo Blog
date: 2017-09-04 23:12:42
tags:
---

## 思路

创建两个分支分别管理 blog 源文件和静态网页.

* git push 推送博客代码到 hexo 分支作为备份


* hexo d 推送静态网页到 master 分支更新博客内容

## 搭建流程

1. 创建仓库: username.github.io

2. 创建两个分支: master 与 hexo

3. 设置 hexo 为默认分支

4. git clone 仓库到本地

5. 在本地 username.github.io 目录下安装 hexo (当前分支为 hexo)

   \* 安装过程中 `hexo init` 会删除 .git 文件夹; 要避免这一问题, 先把 hexo 安装到别的目录, 再拷贝过来即可.

6. 修改 \_config.yml 中的 deploy 参数, 分支应为 master

7. 依次执行 `git add .` `git commit -m "..." ` `git push origin hexo` 提交 blog 源文件到 hexo 分支

8. 执行 `hexo g -d` 生成网站并部署到 master 分支

## 多终端同步 Blog

1. git clone 仓库到本地
2. 在本地 username.github.io 目录下安装 hexo (注: 本次安装不需要 `hexo init` 指令)

\* 只要把 hexo 和所需插件写入到 package.json 中 (安装时加 --save 参数会自动写入), 那么 git clone 下来之后, 只要一句 `npm install` 就能装好 hexo 和所有的依赖

\* 另一台电脑 push, 部署后会改变之前博客的发布时间.

## 关于 Blog 主题的同步

* 使用 git submodules 管理自定义主题
* git push 不会推送自定义主题文件夹中的内容; 解决方法是删除自定义主题目录下的 .git 文件夹, 然后执行 `git rm -rf --cached themes/themename` 清除原本仓库的 git 记录, 使之成为普通文件夹.

**参考文章**

[使用 hexo, 如果换了电脑怎么更新博客? - 回答作者: CrazyMilk] (https://zhihu.com/question/21193762/answer/79109280)

