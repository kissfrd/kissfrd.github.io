---
title: Hexo + Github Pages 搭建静态 Blog
date: 2017-09-04 23:12:42
​---
---

### 配置环境###

####安装 Git

官网下载安装，完成后验证是否安装正确：

```
git --version
```

#####配置 SSH key

首先检查电脑上现有的 ssh key：

```
cd ~/.ssh
```

如提示：`No such file or directory`，则需要生成新的 ssh key。

```
ssh-keygen -t rsa -C "youremail@xxx.xxx"
```

完成后回车，按提示设置密码，密码为空的话提交项目时不用输入。

添加 SSH key 到 Github

打开生成的 `id_rsa.pub`  文件，复制密钥。

登录 Github，添加 SSH key。

验证：

```
ssh -T git@GitHub.com
```

#####配置 Deployment：

```
git config --global user.name "yourname"
git config --global user.email "youremail"
```



####安装 Node.js

官网下载安装，完成后验证是否安装正确：

``` 
node -v
npm -v
```



####安装 Hexo

新建文件夹，在该目录打开命令行

```
npm install hexo-cli -g
```

执行完成后，输入：

```
npm install hexo --save
```

验证：

```
hexo -v
```



#####初始化 Hexo：

```
hexo init
```

执行完成后，输入：

```
npm install
```

自动安装所需组件。



#####查看页面效果

```
hexo g
```

执行完成后，输入：

```
hexo s
```

在浏览器中打开 `http://localhost:4000/`  预览页面。



### 部署静态网页到 Github###

登录 Github，创建 `New repository`，`name` 必须和用户名一致，如：`yourname.github.io` 。

使用 Git 部署至 Github，或使用 GitHub Desktop 同步至 Github。



####使用 Git 部署

安装插件：

```
npm install hexo-deployer-git --save
```

在 `_config.yml`  文件中修改 `Deployment`  部分内容：

```
deploy:
  type: git
  repo: git@github.com:yourname/yourname.github.io.git
  branch: master
```

然后输入：

```
hexo d
```

按提示输入密码开始上传。​

