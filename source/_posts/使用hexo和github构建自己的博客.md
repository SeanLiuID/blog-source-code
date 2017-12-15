---
title: 使用hexo和github构建自己的博客
date: 2017-12-14 22:17:31
categories:
- Hexo
tags:
---
[Hexo中文文档](https://hexo.io/zh-cn/docs/)

## Install Hexo
1. Install Git
``` bash
# for mac
$ brew install git
# for centos
$ sudo yum install git-core
```

2. Install Node.js
``` bash
# install nvm firstly
$ wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
# reboot terminal and install nodejs with nvm
$ nvm install stable
```

3. Install Hexo
``` bash
$ npm install -g hexo-cli
```

## Init Blog Project
``` bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```

## Config Github
1. create a new repository,set repository name to "&lt;githubname&gt;.github.io" strictly.
2. generate ssh key
``` bash
$ ssh-keygen -t rsa -C "youremail@example.com"
$ cd ~/.ssh
$ cat id_rsa.pub
show <ssh key content>
```
3. Enter the settings of repository,copy ssh key which just be generated to "deploy keys" in order to ensure you deploy blog to github directly.
4. To verify whether adding key is success.
``` bash
ssh -T git@github.com
```

## Config Blog Project
1. modify _config.yml
``` bash _config.yml
deploy:
	type: git
    repo: http://github.com/<githubname>/<githubname>.github.io.git
    branch: master
```
2. install deploy tool
``` bash
$ npm install hexo-deployer-git --save
```

## Local Preview

``` bash
$ hexo clean
$ hexo generate
$ hexo server
```
open browser and enter: http://localhost:4000

## Deploy to github
``` bash
$ hexo clean
$ hexo generate
$ hexo deploy
```
open browser and enter: http://&lt;githubname&gt;.github.io